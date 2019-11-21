---
title: Hosting Jekyll web sites with Amazon Lightsail and Let's Encrypt SSL
tags: [Jekyll, SSL, HTTPS, English]
style: fill
color: success
description: Hosting Jekyll web sites with Amazon Lightsail and Let's Encrypt SSL
comments: true
---

Source: [Andy Grove](https://andygrove.io/2018/05/hosting-jekyll-lightsail-lets-encrypt-ssl/)

After the recent fiasco where I moved my web sites from Google Cloud to GitHub Pages and then found out that it wasn’t possible to use a custom domain with SSL with both an apex domain and a www subdomain, I decided to move the sites again this weekend, this time to AWS.

Previously I would have used EC2 but after some quick Googling, it looked like Amazon Lightsail would be a better way to go.

## Creating a Lightsail Instance

I created an Amazon Lightsail instance choosing the “os only” option with Ubuntu 16.04 as my choice of operating system since this is supported well by Let’s Encrypt. I chose the basic hosting plan costing $5 per month. This is more than capable of hosting my sites.

As part of setting up the instance I generated a new SSH key pair and downloaded it (and stored it somewhere safe since this is a one time download). The pem file should be copied to ~/.ssh with a suitable name (I named it id_rsa_lightsail.pem) and you will need to set appropriate permissions using chmod:

```sh
chmod 700 ~/.ssh/id_rsa_lightsail.pem 
```

It is also essential to create a static IP address and associate that with the instance.

## Connecting to the server via SSH

Once the instance had started I was able to connect via SSH using the following command.

```sh
ssh -i ~/.ssh/id_rsa_lightsail.pem ubuntu@18.188.179.245
```

Install Apache Web Server

Install Apache using these commands.

```sh
sudo su -
apt update
apt install apache2
service apache2 start
```

With Apache started, update your local /etc/hosts file and add an entry mapping the server’s static IP address to your domain names.

```sh
18.188.179.245 www.andygrove.io andygrove.io www.datafusion.rs datafusion.rs 
```

You should now see the default Apache web page for a fresh install when accessing your domain from a browser.

## Create Site Content

With the basic infrastructure in place, the next step is to add your content to the server. First, create a directory for each site and set the ownership appropriately.

```sh
cs /var/www
mkdir andygrove.io
mkdir datafusion.rs
chown -R ubuntu:ubuntu *
```

Next, upload the generated content from your Jekyll site. I created the following deploy.sh in each of my Jekyll repos to publish content to the new server, obviously changing the names and paths for each repo.

```sh
bundle exec jekyll clean
bundle exec jekyll build
cd _site
rm -f andygrove.tgz
tar czf andygrove.tgz *
scp -i ~/.ssh/id_rsa_lightsail.pem andygrove.tgz ubuntu@18.188.179.245:
ssh -i ~/.ssh/id_rsa_lightsail.pem ubuntu@18.188.179.245 "cd /var/www/andygrove.io ; tar xzf /home/ubuntu/andygrove.tgz"
```

## Create Virtual Hosts

First, delete the two default files from sites-enabled since they confuse the Let’s Encrypt installer and we don’t need them anyway.

```sh
sudo rm -f /etc/apache2/sites-available/000-default.conf 
sudo rm -f /etc/apache2/sites-available/default-ssl.conf 
```

Now, create one file per domain in /etc/apache2/sites-available. For example, I created andygrove-io.conf with the following contents.

```conf
<VirtualHost *:80>
  ServerName andygrove.io
  ServerAlias www.andygrove.io
  DocumentRoot /var/www/andygrove.io
</VirtualHost>

<VirtualHost *:443>
  ServerName andygrove.io
  ServerAlias www.andygrove.io
  DocumentRoot /var/www/andygrove.io
</VirtualHost>
```

It is then necessary to create a symlink in the sites-enabled directory.

```sh
ln -s /etc/apache2/sites-available/andygrove-io.conf /etc/apache2/sites-enabled/andygrove-io.conf
```

Restart Apache

```sh
service apache2 restart
```

After deploying content I was able to visit the URL for my site and see the correct content.

## Update DNS

Before we can set up SSL we need to now update DNS to point to the new site. Note that this can lead to your site being unavaible for many hours or even a day or two while DNS changes propagate so choose a good time to do this.

Simply create A records for *, @, and www all pointing to the static IP address.

You can use dig to check progress but be aware that it can take up to 72 hours for DNS changes to propagate around the globe.

```sh
dig andygrove.io
```

## Install SSL Certs

Note that SSL certificate creation is only possible once DNS has been updated and Let’s Encrypt servers are able to access your site via DNS.

I followed these instructions on the Let’s Encrypt web site

I chose to generate certificates one site at a time. For example:

```sh
sudo certbot --apache -d andygrove.io -d www.andygrove.io
```

This generated SSL certificates and rewrote my andygrove-io.conf file as follows.

```conf
<VirtualHost *:80>
  ServerName andygrove.io
  ServerAlias www.andygrove.io
  DocumentRoot /var/www/andygrove.io
RewriteEngine on
RewriteCond %{SERVER_NAME} =andygrove.io [OR]
RewriteCond %{SERVER_NAME} =www.andygrove.io
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>

<VirtualHost *:443>
  ServerName andygrove.io
  ServerAlias www.andygrove.io
  DocumentRoot /var/www/andygrove.io
Include /etc/letsencrypt/options-ssl-apache.conf
SSLCertificateFile /etc/letsencrypt/live/andygrove.io/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/andygrove.io/privkey.pem
</VirtualHost>
```

## Summary

That’s it. New sites can easily be added and updating SSL certs from the command line is simple too. Let’s Encrypt will send out email reminders before certs expire.

Overall this process was much less frustrating than using GitHub Pages and at $5 per month for multiple domains it is very affordable.
