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

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/b26a6e15-3e1e-4cf4-89bb-4710c058cb80)

#### Now we will create a file index.js with the command below
`touch index.js`

#### Install the dotenv module
`npm install dotenv`

#### We will Open the index.js file with the command below:
`vim index.js`

#### We will type the code below into it and save.
`const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});`

#### Now it is time to start our server to see if it works. We will open our terminal in the same directory as your index.js file and type:
`node index.js`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/28069cf5-85a5-4a81-82a3-50551688070f)


#### Now we need to open this port in EC2 Security Group. We will ned to created an inbound rule to open TCP port 5000.


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/4720e4e2-7533-4496-9509-68f9737ed2d3)


#### We will Open up our browser and try to access our server’s Public IP or Public DNS name followed by port 5000:


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/3785ce72-85d1-4f23-ae0d-b01e51a6ad4c)

## Routes


#### For each of our task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes
`mkdir routes`

#### We will Change directory to routes folder.
`cd routes`

#### Now, we will create a file api.js with the command below
`touch api.js`

#### We will open the file with the command below
`vim api.js`

#### We will copy below code in the file.
`const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;`

## MODELS

### since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model

#### We will change directory back Todo folder with cd .. and install Mongoose
`npm install mongoose`

#### We will create a new folder models :
`mkdir models`

#### Inside the models folder,we will create a file and name it todo.js
`sudo vim todo.js`

#### We will open the file created with vim todo.js then paste the code below in the file:
`const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;`


#### In Routes directory, we will open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit

`const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;`


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/aa567b1d-9a5f-4e0f-9097-0cc484b9d976)


### MONGODB DATABASE

#### We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up here. Follow the sign up process, select AWS as the cloud provider, and choose a region near you.















