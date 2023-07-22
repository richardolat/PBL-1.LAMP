# CLIENT-SERVER ARCHITECTURE WITH MYSQL

### Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.In their communication, each machine has its own role: the machine sending requests is usually referred as “Client” and the machine responding (serving) is called “Server”.

#### We will Create and configure two Linux-based virtual servers (EC2 instances in AWS).
`Server A name - `mysql server`

`Server B name - `mysql client`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/dac67ce2-c4f1-45fc-a966-f99f34a81273)

#### We will connect to the instances by cd into downloads and copying our ssh-i and private key file and pasting it on our terminals 

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/59839c2e-4ae7-4d17-9a61-14152262ced9)

#### We will run commands to update and upgrade our packages 
`sudo apt update` && `sudo apt upgrade`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/ebc1f9fe-039b-43ac-81c8-3d4a186b84b8)

#### We will set hostname for both Mysql-server and Mysql-client
 `sudo hostnamectl set-hostname mysql-server`
 
 `sudo hostnamectl set-hostname mysql-client`

#### We will exit both and reconnect to allow the hostnames to reflect

`Exit`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/b206568d-50d1-4b97-b455-9813ea850d1d)


#### After restarting it, we will install mysql-server and mysql-client.
`sudo apt install mysql-server`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/30a490d8-4c4c-45e6-a0fb-47262fe0db01)
`sudo apt install mysql-client`

#### We will create username and password on the mysql-client
 `sudo mysql -u richard -p`
 
 ![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/04bec866-d70c-4e0d-9623-b864bf086e15)

#### On the mysql-server, we will enable mysql
 `sudo systemctl enable mysql`

 #### We will enter into mysql by running the command;
` sudo mysql`

#### We will connect to the mysql-client by running the command:
`create user "richard"@"%" identified with mysql_native_password by "buddyrich";`

#### The above include the username and password created for the mysql-client.

#### We will create a database called tooling
` create database tooling;`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/f1201771-69cf-455f-8d44-6e4985bfaa05)

#### We will grant mysql some privileges by running the following commands;
`grant all privileges on tooling.* to "richard"@"%";`

`flush privileges;`

#### We will open the mysql-server file and change the bind address to 0.0.0.0
`sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf`

#### We will go back into mysql and then restart it.
`sudo systemctl restart mysql`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/4104726f-c04e-4b8f-8915-4b2fe5e746e3)


#### In the mysql-client , we will connect to the server and check the database.
 `show databases;`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/33c04820-cd6d-4608-9a1c-3f40e8344bcd)
 



