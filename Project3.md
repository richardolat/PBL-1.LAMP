# SIMPLE TO-DO APPLICATION ON MERN WEB STACK

### MERN Web stack consists of following components:
#### MongoDB: A document-based, No-SQL database used to store application data in a form of documents.

#### ExpressJS: A server side Web Application framework for Node.js.

#### ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

#### Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

## STEP 1 – BACKEND CONFIGURATION

#### Update ubuntu
##### `sudo apt update`

#### Upgrade ubuntu
##### `sudo apt upgrade`

#### Lets get the location of Node.js software from Ubuntu repositories.
##### `curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

#### We will install Node.js on the server
`sudo apt-get install -y nodejs`


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/7b2fe538-6596-421d-8280-a9284118328d)

#### We will verify the node installation with the command below
`node -v `


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/c5807b2f-4a74-4259-b317-066ffbfe3d67)

### Application Code Setup

#### We will create a new directory for our To-Do project:
`mkdir Todo`


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/9bc9f8eb-bdfb-428e-83a0-dfd1dee59ed4)

#### We will use the command `npm init` to initialise your project, so that a new file named package.json will be created.


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/2c864f52-148c-4cbc-a88d-cec765e1a9e0)

## INSTALL EXPRESSJS

#### We will install express using npm
`npm install express`












