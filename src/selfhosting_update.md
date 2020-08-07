# Selfhosting Update

As you know, I was using a Hetzner VPS for hosting various services like Nextcloud, Email and this very blog.
But last night I decided to nuke my VPS and now I'm waiting for my domain to expire.

The main reason I decided to go this route is because my self hosted email was giving me a lot of headaches.
I was constantly worried about mail deliverability. On top of that, It's not like everyone has GPG set up, so I've decided to settle with Tutanota for now.
Tutanota provides 1GB of storage in their basic plan and it provides a way to send encrypted messages to non Tutanota users as well.

Having a VPS just for Cloud and Web Hosting seemed a little excessive to me. So I've shifted my blog to Github Pages and in place of NextCloud, I've set up a very simple DAV Server on my raspberry pi.
For storing some important documents, I'm using `megatools` on my phone and laptop to upload/download files to/from my `Mega.nz` account.

For my domain name, I'm using `dynu`. They provide free subdomains with a DDNS service. So I have a `blahblahblah.dynu.net` domain now and a
bash script running on my pi constantly updates the A records to point to my current IP.

## Generating SSL Certificates

When I started with this process, I was under the impression that generating SSL certificates for my new domain would be a pretty straightforward process using `Certbot`.
But sadly, `Certbot` is not able to pass the ACME challenges for dynu. So instead, I had to use the `acme.sh` script which has a separate plugin for `dynu`.
<br>
To use that plugin, first we need to install the acme.sh script -
```
curl https://get.acme.sh | sh
```

Next, head to the `dynu` control panel and look for the API Credentials option. Then export them as your environment variables as shown -
```
export Dynu_ClientId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
export Dynu_Secret="yyyyyyyyyyyyyyyyyyyyyyyyy"
acme.sh --issue --dns dns_dynu -d mydyndomain.dynu.net
```
And if all work as expected, you will get your certificates.

## Setting Up CardDAV/CalDAV

When I started looking for DAV servers, the application I first came across was `Radicale`. I spent a good hour to set that up but still couldn't get it to behave nicely. IMO don't waste your time with
that application. I'm currently using `Baikal` and it's very nice.

It just needs PHP7, SQlite and Nginx to function. Just extract the latest release from github into your webroot (/var/www/). Then setup a Nginx site as shown -

```
server {
    listen 80;
    server_name blahblahblah.dynu.net;
    return 301 https://blahblahblah.dynu.net$request_uri;
}

server {
  listen 443 ssl;
  server_name blahblahblah.dynu.net;

  ssl_certificate /home/user/.acme.sh/blahblahblah.dynu.net/blahblahblah.dynu.net.cer;
  ssl_certificate_key /home/user/.acme.sh/blahblahblah.dynu.net/blahblahblah.dynu.net.key;

  root /var/www/baikal/html;
  index index.php;

  rewrite ^/.well-known/caldav /dav.php redirect;
  rewrite ^/.well-known/carddav /dav.php redirect;

  charset utf-8;

  location ~ /(\.ht|Core|Specific) {
    deny all;
    return 404;
  }

  location ~ ^(.+\.php)(.*)$ {
    try_files $fastcgi_script_name =404;
    include /etc/nginx/fastcgi_params;
    fastcgi_split_path_info ^(.+\.php)(.*)$;
    fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_param PATH_INFO $fastcgi_path_info;
  }
}
```
and you are done! Just open the URL in your browser and go through the one time admin setup. Then you can create a new user and setup syncing on your phone using `Davx5`.


---

Sources:

- `tutanota`: <https://tutanota.com/>
- `megatools`: <https://megatools.megous.com/>
- `dynu`: <https://www.dynu.com/>
- `baikal`: <https://sabre.io/baikal/>
- `davx5`: <https://www.davx5.com/>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/mananapr.github.io/issues)
</i></center>
