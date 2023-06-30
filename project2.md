# WEB STACK IMPLEMENTATION (LEMP STACK)

### INSTALLING THE NGINX WEB SERVER

#### 1-In order to display web pages to site visitors, we are going to employ Nginx, a high-performance web server.

#### 2-We’ll use the apt package manager to install this package.
`sudo apt update`
`sudo apt install nginx`

#### 3-To verify that nginx was successfully installed and is running as a service in Ubuntu,we will run:
`sudo systemctl status nginx`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/c04b6f4b-6f13-44d3-9aa4-3256243eb06f)

### INSTALLING MYSQL

We will need to install a Database Management System (DBMS) to be able to store and manage data for our site in a relational database 

#### 1-We will use ‘apt’ to acquire and install Mysql-server:
`sudo apt install mysql-server`

#### 2-When the installation is finished, we will log in to the MySQL console by typing:
`sudo mysql`

#### 3-We will start the interactive script by running:
`sudo mysql_secure_installation`

#### 4-When we’re finished,we will test if we’re able to log in to the MySQL console by typing:
`sudo mysql -p`

### INSTALLING PHP

Now we will install PHP to process code and generate dynamic content for the web server.

We will need to install php-fpm and php-mysql

#### 1-To install these 2 packages at once,we will run:
`sudo apt install php-fpm php-mysql`

### CONFIGURING NGINX TO USE PHP PROCESSOR

We will create server blocks (similar to virtual hosts in Apache) to encapsulate configuration details and host more than one domain on a single server.

#### 1-We will create the root web directory for our_domain as follows:
`sudo mkdir /var/www/projectLEMP`

#### 2-We will assign ownership of the directory with the $USER environment variable, which will reference our current system user:
`sudo chown -R $USER:$USER /var/www/projectLEMP`

#### 3-We will open a new configuration file in Nginx’s sites-available directory using our preferred nano command-line editor:
`sudo nano /etc/nginx/sites-available/projectLEMP`

#### 4-We will activate our configuration by linking to the config file from Nginx’s sites-enabled directory:
`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

#### 5-This will tell Nginx to use the configuration next time it is reloaded. We can test our configuration for syntax errors by typing:
`sudo nginx -t`
![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/2a124e96-f797-4b4b-864a-6800c3765f9d)

#### 6- We will reload Nginx to apply the changes:
`sudo systemctl reload nginx`

#### 7-Our new website is now active, but the web root /var/www/projectLEMP is still empty. We will create an index.html file in that location so that we can test that the new server block works as expected:
`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

#### 8-We will then go to our browser and try to open our website URL using IP address:
`http://<Public-IP-Address>:80`
![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/d38619fb-ce22-45e0-88f2-7f8c64a7eb90)

### Testing PHP with Nginx

#### 1-We will creating a test PHP file in our document root. We will open a new file called info.php within our document root in the text editor:
`sudo nano /var/www/projectLEMP/info.php`

#### 2-We will type or paste the following lines into the new file. This is valid PHP code that will return information about our server:
`<?php
phpinfo();`

#### 3-We can now access this page in our web browser by visiting the domain name or public IP address we’ve set up in our Nginx configuration file, followed by /info.php:
`http://`server_domain_or_IP`/info.php`

