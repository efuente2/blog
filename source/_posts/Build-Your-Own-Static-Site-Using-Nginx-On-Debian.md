---
title: Build Your Own Static Site Using Nginx On Debian
date: 2025-02-14 14:07:18
tags:
---

## Prerequisites
 - A Debian-based server
 - Root Or Sudo privileges 

## Step 1: Update Your System
Start by updating your package list and upgrading the system to make sure everything is up-to-date.
``` bash
    sudo apt update && sudo apt upgrade -y
```

## Step 2: Install NGINX
Install NGINX from the official Debian Repo
``` bash
    sudo apt install nginx -y
```

## Step 3: Start and Enable Nginx
Start the NGINX service and enable it to start automatically on boot.
``` bash
    sudo systemctl start nginx 
    sudo systemctl enable nginx
```

## Step 4 (Optional): Allow NGINX Through the Firewall
If running a firewall you need to allow traffic on the HTTP and HTTPS ports
``` bash
    sudo ufw allow 'Nginx Full'
```

## Step 5: Create a Directory for Your Website
Create a directory to store your static website files. For example, we create a website directory.
``` bash
    sudo mkdir -p /var/www/mywebsite/html
```

## Step 6: Add Your Website Files
Now, place your website's file (HTML, CSS, JS, image, etc) into the directory you just created.
For Example, let's create a simple index.html file
``` bash
    echo "<html><head><title>My Website</title></head><body><h1>Welcome to My Website</h1></body></html>" | sudo tee /var/www/mywebsite/html/index.html > /dev/null
```
## Step 7: Set Permissions 
Set the appropriate ownership and permission for the web directory 
``` bash
    sudo chown -R www-data: www-data /var/www/mywebsite/html
    sudo chmod -R 755 /var/www/mywebsite
```

## Step 8: Configure NGINX for Your Website 
Now, you need to create a new configuration file for your website. NGINX configuration files are located
in /etc/nginx/sites-available/ and /etc/nginx/site-enabled/
Create a new file for your website under /etc/nginx/site-available/:
``` bash
    sudo nano /etc/nginx/site-available/mywebsite
```
Add the following configuration to the file:
``` bash
    server {
        listen 80;
        server_name mywebsite.com www.mywebsite.com;  # Replace with your domain name or IP address

        root /var/www/mywebsite/html;  # Path to your website directory
        index index.html;

        location / {
            try_files $uri $uri/ =404;
        }
    }
```

## Step 9: Enable the Site
Create a symbolic link in the site-enable directory to enable the site.
``` bash
    sudo ln -s /etc/nginx/sites-available/mywebsite /etc/nginx/sites-enabled/
```

## Step 10: Test the NGINX Configuration 
Before restarting NGINX, its important to test the configuration for syntax errors.
``` bash
    sudo nginx -t
```
If there are no errors, you'll see a message saying that the syntax is ok. If there are errors, resolve them before proceeding.

## Step 11: Restart NGINX
Restart NGINX to apply the new configuration
``` bash
    sudo systemctl restart nginx
```

## Step 12: Access Your Website 
Now, open a web browser and navigate to your server's IP address or domain name (e.g.,
http://your_server_ip or http://mywebsite.com). You Should see your static website!

## Step 13: Optional - Setting Up SSL with Let's Encrypt (HTTPS)
For enhanced security, you might want to set up SSL using Let's Encrypt. Here how you can do that:
1. Install Certbot:
``` bash
    sudo apt install certbot python3-certbot-nginx -y
```
2.Obtain an SSL certificate:
``` bash
    sudo certbot --nginx -d mywebsite.com -d www.mywebsite.com
```
3.Certbot will automatically configure SSL for your NGINX server and reload it.

## Step 14: Renewing SSL Certificates 
Let's Encrypt certificates expires after 90 days, so it's essential to renew them. You can set up a cron job
to automatically renew the certificate:
``` bash
    sudo crontab -e
```
Add the following line to check for renewals twice a day:
``` bash
    0 12 * * * certbot renew --quiet
```