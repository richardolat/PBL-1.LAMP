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

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/6e55e2c5-b35d-442d-afb6-89386080da09)


#### We will create a new folder models :
`mkdir models`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/38c3a302-2f17-449d-b597-12f84273ed2a)


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


### MONGODB DATABASE

#### We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. 

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/5a886e92-7e54-491a-bdaa-e01d684e4948)


#### We will create a file in our Todo directory and name it .env.
`touch .env`
`vi .env`

#### We will add the connection string to access the database in it, just as below:

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/58cba98e-ebf9-413d-868f-360f86338edf)


#### We will need to update the index.js to reflect the use of .env so that Node.js can connect to the database.
#### We will Open the file with` vim index.js`

#### The entire content in it will be deleted, then we will paste the entire code below in the file.

`const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});`

#### We will start your server using the command:
`node index.js`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/4ba4839b-3a3d-42e8-b8f0-fcec52f20579)

## Testing Backend Code without Frontend using RESTful API

#### In this project, we will use Postman to test our API.

#### Now we will open our Postman and create a POST request to the API

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/1ad719ce-b616-4ef7-9d6e-40498081dbfa)


#### We will create a GET request to our API 

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/1cccc669-6405-4ec7-aa59-73756eeaa8eb)

## FRONTEND CREATION

#### In the same root directory as our backend code, which is the Todo directory, we will run:

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/4dbe632a-f101-4876-af71-6981daab353d)

#### We will install concurrently. It is used to run more than one command simultaneously from the same terminal window.
`npm install concurrently --save-dev`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/baa3a40a-66cd-4cae-9c88-54bc2a55658f)


#### We will install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
`npm install nodemon --save-dev`
![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/aec0bcc5-f02c-4e84-9ff3-46d664715991)

#### In Todo folder, we will open the package.json file. We will Change the script part and replace with the code below."scripts": {
`"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},`

#### We will Change directory to ‘client’

#### We will open the package.json file

#### We will add the key value pair in the package.json file "proxy": "http://localhost:5000".

#### Now,we will  ensure we are inside the Todo directory, and simply do:
`npm run dev`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/835e2360-b901-482e-972b-9fdec95dc93f)


#### From our Todo directory run;
`cd client`

#### We will move to the src directory
`cd src`

#### Inside our src folder create another folder called components
`mkdir components`

#### We will move into the components directory with:
`cd components`

#### Inside ‘components’ directory we will  create three files Input.js, ListTodo.js and Todo.js.
`touch Input.js ListTodo.js Todo.js`

#### We will Open Input.js file
`vi Input.js`

#### Then we input the following:

`import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input`

#### We will install Axios
`npm install axios`
































