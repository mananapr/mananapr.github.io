# Setting up your own Mail Server

Configuring and running your own email server is a major pain in the ass. So, I wanted to write a post about
setting one up, mainly to document all the things I did while setting one up for myself. Hopefully this guide
helps someone else as well.

Depending on your VPS provider and your OS, you might have to do some other things as well.
I use an `Ubuntu 18.04 LTS` VPS provided by `Hetzner`.

## List of Services

 - Postfix for SMTP
 - Dovecot for IMAP
 - MariaDB for Database
 - LetsEncrypt/Certbot for SSL Certificates

## DNS Settings

For the entirety of this post, I am going to assume that your domain is `yourdomain.com`.
Open up your DNS provider's dashboard and create a new MX record as follows:

```
mail.yourdomain.com    MX      10      YOUREXTERNALIPADDRESS
```

## Installing Packages

Next, We'll install the packages I mentioned above by running:

```
sudo apt-get install certbot postfix postfix-mysql dovecot-core dovecot-imapd dovecot-pop3d dovecot-lmtpd dovecot-mysql mariadb-server
```

While installation, you'll be prompted to enter a password for the root MySQL user as well as set a configuration type for Postfix (Go with Internet Site).

## Generating SSL Certificates

We'll be generating SSL certificates using Certbot/LetsEncypt. To generate the ceritificates, run:

```
sudo certbot -d yourdomain.com -d mail.yourdomain.com
```

To automatically renew the certificates, you can set a cronjob for `cerbot renew`.


## Configuring MariaDB

We have to create a database that will have tables for domains, email addresses/passwords and email aliases.
We'll also create a dedicated MySQL user for Postfix and Dovecot.

#### Creating the Database and Tables

To create the database, run the following command:

```
sudo mysqladmin -p create mailserver
```

Then login to the MySQL commandline using:

```
sudo mysql -p mailserver
```

Next, we'll create a new MySQL user (mailuser in this case) by entering the following command:

```
GRANT SELECT ON mailserver.* TO `mailuser`@`127.0.0.1` IDENTIFIED BY `mailuserpass`;
FLUSH PRIVILEGES;
```


Enter the following command to create a table for the domains that will receive mail on your server:

```
CREATE TABLE `virtual_domains` (`id` int(11) NOT NULL auto_increment, `name` varchar(50) NOT NULL, PRIMARY KEY (`id`)) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Enter the following command to create a table for all of the email addresses and passwords:

```
CREATE TABLE `virtual_users` (`id` int(11) NOT NULL auto_increment, `domain_id` int(11) NOT NULL, `password` varchar(106) NOT NULL, `email` varchar(100) NOT NULL, PRIMARY KEY (`id`), UNIQUE KEY `email` (`email`), FOREIGN KEY (domain_id) REFERENCES virtual_domains(id) ON DELETE CASCADE) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Enter the following command to create a table for your email aliases:

```
CREATE TABLE `virtual_aliases` (`id` int(11) NOT NULL auto_increment,`domain_id` int(11) NOT NULL,`source` varchar(100) NOT NULL,`destination` varchar(100) NOT NULL,PRIMARY KEY (`id`),FOREIGN KEY (domain_id) REFERENCES virtual_domains(id) ON DELETE CASCADE) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

With this, we're done with creating the tables.

#### Adding Data

Now that we've created the database and tables, we have to add some data in the tables.

Add your domains to the virtual_domains table. You can add as many domains as you want in the VALUES section of the command below:

```
INSERT INTO mailserver.virtual_domains (id ,name) VALUES ('1', 'yourdomain.com'), ('2', 'mail.yourdomain.com');
```

Make a note of which id goes with which domain.

Next, Add email addresses to the virtual_users table:

```
INSERT INTO mailserver.virtual_users (id, domain_id, password , email) VALUES ('1', '1', ENCRYPT('USERPASSWORD', CONCAT('$6$', SUBSTRING(SHA(RAND()), -16))), 'USEREMAIL@yourdomain.com');
```

To add email alias to the virtual_aliases table, run the following query:

```
INSERT INTO mailserver.virtual_aliases (id, domain_id, source, destination) VALUES ('1', '1', 'alias@yourdomain.com', 'USEREMAIL@yourdomain.com');
```

With this, we're finished with the MySQL configuration.

## Postfix Configuration

Postfix has two config files: `/etc/postfix/main.cf` & `/etc/postfix/master.cf`. I would recommend taking a backup of the original config files before
proceeding so that you can undo any changes if things go wrong.

Start by editing the `/etc/postfix/main.cf` as shown below:

```
# TLS parameters
smtpd_tls_cert_file=/etc/letsencrypt/live/yourdomain.com/fullchain.pem
smtpd_tls_key_file=/etc/letsencrypt/live/yourdomain.com/privkey.pem
smtpd_use_tls=yes
smtpd_tls_security_level = may
smtp_tls_security_level = may
smtpd_tls_session_cache_database = btree:${data_directory}/smtpd_scache
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache

# Authentication
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_sasl_auth_enable = yes

# See /usr/share/doc/postfix/TLS_README.gz in the postfix-doc package for
# information on enabling SSL in the smtp client.

smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
myhostname = mail.yourdomain.com
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
mydomain = mail.yourdomain.com
myorigin = $mydomain
mydestination = $myhostname, localhost.localdomain, localhost
relayhost =
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
inet_protocols = all

# Handing off local delivery to Dovecot's LMTP, and telling it where to store mail
virtual_transport = lmtp:unix:private/dovecot-lmtp

# Virtual domains, users, and aliases
virtual_mailbox_domains = mysql:/etc/postfix/mysql-virtual-mailbox-domains.cf
virtual_mailbox_maps = mysql:/etc/postfix/mysql-virtual-mailbox-maps.cf
virtual_alias_maps = mysql:/etc/postfix/mysql-virtual-alias-maps.cf,
        mysql:/etc/postfix/mysql-virtual-email2email.cf
```

Now we have to tell Postfix how to connect to MySQL.

For connecting virtual domains, create the file `/etc/postfix/mysql-virtual-mailbox-domains.cf`

```
user = mailuser
password = mailuserpass
hosts = 127.0.0.1
dbname = mailserver
query = SELECT 1 FROM virtual_domains WHERE name='%s'
```

Similarly, for email address connection, create the file `/etc/postfix/mysql-virtual-mailbox-maps.cf`

```
user = mailuser
password = mailuserpass
hosts = 127.0.0.1
dbname = mailserver
query = SELECT 1 FROM virtual_users WHERE email='%s'
```

Finally, for aliases connection, create the file `/etc/postfix/mysql-virtual-alias-maps.cf`

```
user = mailuser
password = mailuserpass
hosts = 127.0.0.1
dbname = mailserver
query = SELECT destination FROM virtual_aliases WHERE source='%s
```

Restart postfix by typing,

```
sudo systemctl restart postfix
```

Now, to verify if the connections are working, try the following commands:

```
postmap -q yourdomain.com mysql:/etc/postfix/mysql-virtual-mailbox-domains.cf
postmap -q email@yourdomain.com mysql:/etc/postfix/mysql-virtual-mailbox-maps.cf
postmap -q alias@yourdomain.com mysql:/etc/postfix/mysql-virtual-alias-maps.cf
```

You should get an output for each of the commands. If nothing is returned, you have some error.

Now we'll edit the second config file, `/etc/postfix/master.cf`. Make sure the following lines are uncommented:

```
smtp      inet  n       -       y       -       -       smtpd
submission inet n       -       y       -       -       smtpd
smtps     inet  n       -       y       -       -       smtpd
  -o syslog_name=postfix/smtps
  -o smtpd_tls_wrappermode=yes
  -o smtpd_sasl_auth_enable=yes

```

This enables SMTP over STARTTLS (Ports 25 & 587) as well as SMTP over SSL/TLS (Port 465). You should use SMTP
over SSL/TLS (Port 465) for sending mails as it is more secure than STARTTLS.

Restart the postfix service and make sure it starts without any errors.

With this we are done with Postfix configuration (at least for now).

## Dovecot Configuration

Like postfix, I would recommend taking backup of every config file you edit.

Firstly, open the main dovecot config file `/etc/dovecot/dovecot.conf` and check if the following lines are present
and uncommented:

```
!include_try /usr/share/dovecot/protocols.d/*.protocol
protocols = imap lmtp
!include conf.d/*.conf
!include_try local.conf
```

Now we'll configure how dovecot stores the emails. Open `/etc/dovecot/conf.d/10-mail.conf` and set `mail_location` as per your preference.
I have it set as follows:

```
mail_location = maildir:/data/mail/vhosts/%d/%n
```

`%d` is the domain and `%n` is the email id. Make sure the location you provide exists and has the correct permissions.
So, in my case,

```
sudo mkdir /data/mail
sudo mkdir -p /data/mail/vhosts/yourdomain.com
sudo groupadd -g 5000 vmail
sudo useradd -g vmail -u 5000 vmail -d /data/mail
sudo chown -R vmail:vmail /data/mail
```

makes the directory and sets correct permissions for the same. The `vmail` user will be responsible for reading mail from the server.

Now let's setup authentication in dovecot so that only authenticated users can read the emails. Start by opening `/etc/dovecot/conf.d/10-auth.conf`
and make sure the following variables are setup as shown:

```
disable_plaintext_auth = yes
auth_mechanisms = plain login
#!include auth-system.conf.ext
!include auth-sql.conf.ext
```

Now, let's create `/etc/dovecot/conf.d/auth-sql.conf.ext` with the authentication information:

```
passdb {
  driver = sql
  args = /etc/dovecot/dovecot-sql.conf.ext
}
userdb {
  driver = static
  args = uid=vmail gid=vmail home=/data/mail/vhosts/%d/%n
}
```

We'll also have to update `/etc/dovecot/dovecot-sql.conf.ext` with our custom MySQL connection information:

```
driver = mysql
connect = host=127.0.0.1 dbname=mailserver user=mailuser password=mailuserpass
default_pass_scheme = SHA512-CRYPT
password_query = SELECT email as user, password FROM virtual_users WHERE email='%u';
```

Next, change the owner and group of the `/etc/dovecot/` directory to `vmail` and `dovecot` by entering the following command:

```
chown -R vmail:dovecot /etc/dovecot
```

Also, change the permissions on the `/etc/dovecot/` directory by entering the following command:

```
chmod -R o-rwx /etc/dovecot
```

Next, we'll have to configure LMTP socket for local mail delivery and the auth socket for authentication in `/etc/dovecot/conf.d/10-master.conf`:

```
service imap-login {
  inet_listener imap {
    port = 0
  }
  inet_listener imaps {
    #port = 993
    #ssl = yes
  }
}

service pop3-login {
  inet_listener pop3 {
    port = 0
  }
  inet_listener pop3s {
    #port = 995
    #ssl = yes
  }
}

service lmtp {
  unix_listener /var/spool/postfix/private/dovecot-lmtp {
    mode = 0666
    user = postfix
    group = postfix
  }
}

service auth {
  unix_listener auth-userdb {
    mode = 0666
    user = vmail
    group = vmail
  }

  # Postfix smtp-auth
  unix_listener /var/spool/postfix/private/auth {
    mode = 0666
    user = postfix
    group = postfix
  }

  # Auth process is run as this user.
  user = dovecot
}

service auth-worker {
  # Auth worker process is run as root by default, so that it can access
  # /etc/shadow. If this isn't necessary, the user should be changed to
  # $default_internal_user.
  user = vmail
}
```

To configure SSL, we'll have to edit `/etc/dovecot/conf.d/10-ssl.conf`:

```
ssl = required
ssl_cert = </etc/letsencrypt/live/yourdomain.com/fullchain.pem
ssl_key = </etc/letsencrypt/live/yourdomain.com/privkey.pem
ssl_client_ca_dir = /etc/ssl/certs
ssl_protocols = !SSLv2 !SSLv3
```

Finally, open the file `/etc/dovecot/conf.d/15-lda.conf` for one last setting:

```
postmaster_address = %d
```

Restart dovecot by entering the following command:

```
sudo service dovecot restart
```

That's It. If email sending and receiving works, then go on to the next part of this guide.
Else, check for logs using,

```
sudo tail -f /var/log/mail.log
```

There's a catch though -  we haven't set up things like `SPF`, `DKIM`, `DMARC` and `rDNS`.
Setting these up makes it possible for the recipient server to verify if the sender is verified
or if someone is just spoofing the sender domain. `DKIM` in particular also lets mail servers detect if
your mail has been tampered with in transit. Linode has a great article on this which I'll link to at the bottom.

It is mandatory to set up SPF, DKM and DMARC if you don't want your emails to go into receiver's spam folder, so follow the
linode article linked at the end.

## General Tips

 - Check if your IP is in blacklists.
 - Send an Email to a GMail address. When viewing that mail in GMail, select the "Show Original Message" option. It will show you if your mail passes SPF, DKIM and DMARC.
 - Set up Reverse DNS records for your IPv4 address and IPv6 address (if applicable).
 - Test your configurations at several online email testers.

---

Sources:

- `setting up spf, dkim & dmarc`: <https://www.linode.com/docs/email/postfix/configure-spf-and-dkim-in-postfix-on-debian-8/>
- `email tester`: <https://www.mail-tester.com/>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/blog/issues)
</i></center>
