# Services I Self Host

Recently, I invested in a VPS to self host a few services in order move away from
proprietary services like Google for eg. I bought a `Hetzner` Cloud VPS because they are
based in Germany and hence follow EU data protection laws. I got my hostname from `namecheap`
for dirt cheap :)

## List of Servies

 - Cloud
 - Email
 - Paste Service
 - IRC Client
 - This blog and other Webservices

## Cloud

I self host `Nextcloud` to get a personal cloud storage with features like
Office, Notes, Contacts & Calendar.

On android, I have `DAVx5` installed to sync my contacts and calendar with Nextcloud instance using `CalDAV` and `WebDAV`.
To sync my notes, `Orgzly` has an option to sync using a remote `WebDAV` repo which does the job.
I also have an `Collabra Office` server that is configured to work with Nextcloud. This makes a pretty good alternative to the GDocs Suite.

Sadly, `Nextcloud` doesn't has an official cli client. Therefore, I use `rclone` with WebDAV to manage my cloud from the cli.

## Email

If you've ever tried hosting an email server, you know it's a real pain in the ass.
There are a lot of moving parts in a mail server and on top of that, you also have to configure
things like `SPF`, `DMIK` and `DMARC` so that your mails don't get marked as spam.
This has been the most headache inducing part of my self hosting experience to be honest.

I use the `Postfix` + `Dovecot` + `MariaDB` + `OpenDKIM` stack to send and recieve mails.
I haven't installed a webclient like `Roundcube` or `Rainloop` because it's extra headache. The SMTP and IMAP
services can be used using any mail client so that's not an issue.

On Android I use `K9-Mail` and on my laptop I just use Nextcloud's Email app.

## Paste Service

I've always wanted a simple pastebin service that is terminal friendly.
`fiche` is a simple pastebin service that I found which allows users
to send information to it using netcat. So a simple,
```
    echo just testing! | nc paste.mananapr.xyz 9999
```
is what I need to do. As I can pipe anything into `netcat`, this makes pasting
things so much easier.

## Blog

I use `nginx` to serve this blog with `ssl`. The certificates were generated using `LetsEncrypt`.
The certificates are valid for this blog, my mail, fiche and nextcloud.

To generate these html pages, I use a simple bash script that compiles markdown to html using `pandoc`.
The script can be found at the blog's github repo which I will link in the sources.

## IRC

I run `weechat` in a `screen` instance so that I am always logged into the IRC channels. Earlier, I used to use
my Raspberry Pi for this but now I have migrated to my VPS due to better uptime.

---

Sources:

- `Hetzner`: <https://www.hetzner.com/>
- `Namecheap`: <https://www.namecheap.com/>
- `Nextcloud`: <https://nextcloud.com/>
- `fiche`: <https://github.com/solusipse/fiche>
- `Postfix`: <http://www.postfix.org/>
- `Dovecot`: <https://www.dovecot.org/>
- `rclone`: <https://rclone.org/>
- `Blog`: <https://github.com/mananapr/blog>
