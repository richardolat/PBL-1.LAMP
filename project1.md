# PBL-PROJECT1

1- In order to complete this project, we need to setup an AWS account and a virtual server with Ubuntu Server OS.

2- AWS is the biggest Cloud Service Provider and it offers a free tier account that we are going to leverage for our projects.

### INSTALLING APACHE AND UPDATING THE FIREWALL

1- What exactly is Apache?

Apache HTTP Server is the most widely used web server software. Developed and maintained by Apache Software Foundation, Apache is an open source software available for free. It runs on 67% of all webservers in the world.

We need to Install Apache using Ubuntu’s package manager ‘apt’:

#### 1-We will update a list of packages in package manager
`sudo apt update`

#### 2-We will run apache2 package installation
`sudo apt install apache2`

#### 3-To verify that apache2 is running as a Service in our OS,we will run the following command
`sudo systemctl status apache2`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/fd58fa29-d25b-42ef-8cdf-1bb57f1a819d)

### INSTALLING MYSQL

MySQL is a popular relational database management system used within PHP environments, so we will use it in our project.

#### 1-We will use ‘apt’ to acquire and install mysql:
`sudo apt install mysql-server`

#### 2-When the installation is finished, we will log in to the MySQL console by typing:
`sudo mysql`

#### 3-We will Start the interactive script by running:
`sudo mysql_secure_installation`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/d13eeb2f-4ad6-4a57-b9c9-58871405710f)


###  INSTALLING PHP

PHP is the component of our setup that will process code to display dynamic content to the end user. In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need libapache2-mod-php to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.

#### 1-We will install these 3 packages at once;
`sudo apt install php libapache2-mod-php php-mysql`

#### Once the installation is finished, we will run the following command to confirm our PHP version:
`php -v`



### CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE




