---
description: Sunucu tarafındaki bilgilerimi geliştirmek için oluşturduğum kısayollardır.
---

# Linux Ubuntu Çalışma Notlarım

## LINUX COMMANDS

### Lınux Basics

* **COPY** 
  * `cp index.js node-server/` to the directory
  * `cp index.js main.js` to the current directory
* **Restart:**  `sudo reboot`
* **Update-Upgrade** `sudo apt-get update`  `sudo apt-get upgrade` 
* **Switch User** `su - afozbek`
* **Add SSH KEY** `nano ~/.ssh/authorized_keys`
* **Enable Firewall** `sudo ufw enable`
  * **List** `sudo ufw app list`
    * * **Nginx Full**: This profile opens both port 80 \(normal, unencrypted web traffic\) and port 443 \(TLS/SSL encrypted traffic\)
    * **Nginx HTTP**: This profile opens only port 80 \(normal, unencrypted web traffic\)
    * **Nginx HTTPS**: This profile opens only port 443 \(TLS/SSL encrypted traffic\)

      **NGINX \(LIKE APACHE\) - Reverse Proxy**

      [What is a Reverse Proxy Server? \| NGINX](https://www.nginx.com/resources/glossary/reverse-proxy-server/)

      [Node app deploy with nginx & SSL · GitHub](https://gist.github.com/bradtraversy/cd90d1ed3c462fe3bddd11bf8953a896)
* **Stop** `sudo systemctl stop nginx`
* **Restart** `service nginx restart`
* **Start** `sudo systemctl start nginx`
  * HTML dosyası: `/var/www/html`
* `/etc/nginx`: The Nginx configuration directory. All of the Nginx configuration files reside here.
* `/etc/nginx/nginx.conf` The main Nginx configuration file. This can be modified to make changes to the Nginx global configuration.
  * Access Log: `/var/log/nginx/access.log`
  * Error Log: `/var/log/nginx/error.log`
* `/etc/nginx/sites-available/`: The directory where per-site “server blocks” can be stored. Nginx will not use the configuration files found in this directory unless they are linked to the sites-enabled directory \(see below\). 
* `/etc/nginx/sites-enabled/`: The directory where enabled per-site “server blocks” are stored. 
* `/etc/nginx/snippets`: This directory contains configuration fragments that can be included elsewhere in the Nginx configuration.

### **PM2**

* `pm2 stop app_name_or_id`
* `pm2 list`
* `pm2 info app`
* To Start All instance on startup `pm2 startup ubuntu`
* [PM2 - Single Page Doc](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/)

### Nano

1. `CTRL + 6` for Mark Set and mark what you want \(the end could do some extra help\).
2. `ALT + 6` copy selected line
3. `CTRL + K` for cutting what you want to copy
4. `CTRL + U` for pasting what you have just cut because you just want to copy.
5. `CTRL + U` at the place you want to paste.

