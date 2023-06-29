# PBL-PROJECT1

1- In order to complete this project, we need to setup an AWS account and a virtual server with Ubuntu Server OS.

2- AWS is the biggest Cloud Service Provider and it offers a free tier account that we are going to leverage for our projects.

### INSTALLING APACHE AND UPDATING THE FIREWALL

1- What exactly is Apache?

Apache HTTP Server is the most widely used web server software. Developed and maintained by Apache Software Foundation, Apache is an open source software available for free. It runs on 67% of all webservers in the world.

We need to Install Apache using Ubuntu’s package manager ‘apt’:

#### 1-update a list of packages in package manager
`sudo apt update`

#### 2-run apache2 package installation
`sudo apt install apache2`


To verify that our apache2 is running as a Service in our OS, we will run the following command;
`sudo systemctl status apache2`
