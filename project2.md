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

When using the Nginx web server, we can create serve
