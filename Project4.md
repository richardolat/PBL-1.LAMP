# MEAN STACK DEPLOYMENT TO UBUNTU IN AWS

##  MEAN Stack is a combination of following components:
#### 1 MongoDB (Document database) – Stores and allows to retrieve data.
#### 2 Express (Back-end application framework) – Makes requests to Database for Reads and Writes.
#### 3 Angular (Front-end application framework) – Handles Client and Server Requests
#### 4 Node.js (JavaScript runtime environment) – Accepts requests and displays results to end user

### Step 1: Install NodeJs

#### We will Update ubuntu
`sudo apt update`

#### We will upgrade ubuntu
`sudo apt upgrade`

#### We will add certificates
`sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates`
`curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/98778f89-2df6-4f9c-92cd-75c43bc0026b)

#### We will then install NodeJS
`sudo apt install -y nodejs`

### Step 2: Install MongoDB
#### MongoDB stores data in flexible, JSON-like documents.

#### We are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.
`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/40aab6b8-c8c4-46da-b3e4-ffe67739cd0a)







