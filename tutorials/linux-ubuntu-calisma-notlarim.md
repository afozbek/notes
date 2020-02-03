---
description: "I have added the shortcuts I learned while developing my server side information to this article content. I hope that will be useful \U0001F607"
---

# Helpful Linux Commands

## LINUX COMMANDS

* **COPY**
  * `cp index.js node-server/` to the directory
  * `cp index.js main.js` to the current directory
* **Restart:**  `sudo reboot`
* **Update-Upgrade** `sudo apt-get update`  `sudo apt-get upgrade` 
* **Switch User** `su - afozbek`
* **User Add** `useradd afozbek-simple`
  * `adduser afozbek`
* **List Users** `nano /etc/passwd`
* **Delete User** `deluser —remove-home newuser`
* **Add Password to User** `passwd afozbek-simple`
* **Add SSH KEY** `sudo nano ~/.ssh/authorized_keys`
* **Change SSH Config** `sudo nano /etc/ssh/sshd_config`
* **Enable Firewall** `sudo ufw enable`
  * **List** `sudo ufw app list`
    * * **Nginx Full**: This profile opens both port 80 \(normal, unencrypted web traffic\) and port 443 \(TLS/SSL encrypted traffic\)
    * **Nginx HTTP**: This profile opens only port 80 \(normal, unencrypted web traffic\)
    * **Nginx HTTPS**: This profile opens only port 443 \(TLS/SSL encrypted traffic\)
* **Look for System is Working Properly**
  * `sudo systemctl status sshd`
  * `sudo systemctl restart ssh`

### **NGINX \(LIKE APACHE\) - Reverse Proxy**

{% embed url="https://www.nginx.com/resources/glossary/reverse-proxy-server/" caption="" %}

> [Nginx installation tutorial](https://gist.github.com/bradtraversy/cd90d1ed3c462fe3bddd11bf8953a896)

* **Stop** `sudo systemctl stop nginx`
* **Restart** `service nginx restart`
* **Start** `sudo systemctl start nginx`
  * Default HTML location: `/var/www/html`
* `/etc/nginx`: The Nginx configuration directory. All of the Nginx configuration files reside here.
* `/etc/nginx/nginx.conf` The main Nginx configuration file. This can be modified to make changes to the Nginx global configuration.
  * Access Log: `/var/log/nginx/access.log`
  * Error Log: `/var/log/nginx/error.log`
* `/etc/nginx/sites-available/`: The directory where per-site “server blocks” can be stored. Nginx will not use the configuration files found in this directory unless they are linked to the sites-enabled directory \(see below\). 
* `/etc/nginx/sites-enabled/`: The directory where enabled per-site “server blocks” are stored. 
* `/etc/nginx/snippets`: This directory contains configuration fragments that can be included elsewhere in the Nginx configuration.

  **PM2**

* `pm2 stop app_name_or_id`
* `pm2 list`
* `pm2 info app`
* To Start All instance on startup `pm2 startup ubuntu`

{% embed url="https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/" caption="Pm2 Docs" %}

### Nano

1. `CTRL + 6` for Mark Set and mark what you want \(the end could do some extra help\).
2. `ALT + 6` copy selected line
3. `CTRL + K` for cutting what you want to copy
4. `CTRL + U` for pasting what you have just cut because you just want to copy.
5. `CTRL + U` at the place you want to paste.

### DOCKER

{% embed url="https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04" caption="How to install docker to your droplet" %}

1. Add User to Docker Group `sudo usermod -aG docker username`
2. Check User is in the Docker Group `id -nG`
3. To view system-wide information about Docker, use: `docker info`
4. Find and download\(if not exist\) an image from Docker Hub: `docker run {image}`
   1. Ex: `docker run hello-world`
5. Search and list images : `docker search {image}`
   1. Ex: `docker search ubuntu`
6. Run a Container and switch to the **interactive terminal\(-it\)**
   1. `docker run -it ubuntu`
7. Listing containers
   1. List running containers  `docker ps`
   2. List stopped containers `docker ps -f “status=exited”`
   3. List all containers `docker ps -a`
   4. View latest container `docker ps -l`
8. Start or Stop a container with its **containerId**
   1. `docker start {containerId}`
   2. `docker stop {containerId}`
9. Remove a container  with its **containerId** or **name**
   1. `docker rm {containerId}`
   2. `docker rm {name}`
10. Remove an image with its **imageId** or **name**
    1. `docker rmi {imageId}`
    2. `docker rmi {name}`
11. Start a container with giving a custom name with **—name**
    1. `docker run --name newName {imageName}`
12. Manage your changes
    1. Commit: `docker commit -m "added Node.js" -a "{userName}" {containerId} "{userName}"/{newImageName}`
    2. Push `docker push {userName}/{imageName}`
13. Listing the Docker images - \(You can see your new image there 😁\)
    1. `docker images`
14. Login to Docker Hub
    1. `docker login -u {docker-registry-username}`

