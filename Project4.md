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
![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/98778f89-2df6-4f9c-92cd-75c43bc0026b)

`curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/825c55d1-0bff-4d56-8bf9-f8ab99e62602)

#### We will then install NodeJS
`sudo apt install -y nodejs`

### Step 2: Install MongoDB
#### MongoDB stores data in flexible, JSON-like documents.

#### We are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.
`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`

`echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list`

#### We will install MongoDB
`sudo apt install -y mongodb`


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/40aab6b8-c8c4-46da-b3e4-ffe67739cd0a)

#### We will start The server
`sudo service mongodb start`

#### We will verify that the service is up and running
`sudo systemctl status mongodb`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/4a31dfd4-4e72-4baa-a1cb-9bf39b6e10b1)


#### We will install npm – Node package manager.
`sudo apt install -y npm`

#### I encounter some challenges installing the npm. i got the following errors;

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/34d15d3c-2772-453b-9529-7aa830360691)

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/b278950e-922e-4a73-9c7b-bc09480beb0a)

#### I tried a lot of options and commands but still didnt work. i finally installed aptitude 
` sudo apt-get install aptitude`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/d3569d93-6c69-4687-9df6-9c8cc3a21a34)

#### I now used aptitude to install npm
` sudo aptitude install npm`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/429dc42a-aee3-434f-8584-8fb6d3a5419c)


#### We will install body-parser package
`sudo npm install body-parser`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/729cc5b7-bcf0-422e-9cca-56942ec53bc8)


#### We will create a folder named ‘Books’
`mkdir Books && cd Books`

#### In the Books directory, we will initialize npm project
`npm init`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/d65d2e14-ebf9-4713-94a7-42b7af295998)

#### We will add a file to it named server.js
`vi server.js`

#### Copy and paste the web server code below into the server.js file.
`var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});`


### Step 3: Install Express and set up routes to the server
`sudo npm install express mongoose`

#### In ‘Books’ folder,we will create a folder named apps
`mkdir apps && cd apps`

#### We will create a file named routes.js
`vi routes.js`

#### We will copy and paste the code below into routes.js
`const Book = require('./models/book');

module.exports = function(app){
  app.get('/book', function(req, res){
    Book.find({}).then(result => {
      res.json(result);
    }).catch(err => {
      console.error(err);
      res.status(500).send('An error occurred while retrieving books');
    });
  });

  app.post('/book', function(req, res){
    const book = new Book({
      name: req.body.name,
      isbn: req.body.isbn,
      author: req.body.author,
      pages: req.body.pages
    });
    book.save().then(result => {
      res.json({
        message: "Successfully added book",
        book: result
      });
    }).catch(err => {
      console.error(err);
      res.status(500).send('An error occurred while saving the book');
    });
  });

  app.delete("/book/:isbn", function(req, res){
    Book.findOneAndRemove(req.query).then(result => {
      res.json({
        message: "Successfully deleted the book",
        book: result
      });
    }).catch(err => {
      console.error(err);
      res.status(500).send('An error occurred while deleting the book');
    });
  });

  const path = require('path');
  app.get('*', function(req, res){
    res.sendFile(path.join(__dirname, 'public', 'index.html'));
  });
};`

#### In the ‘apps’ folder,we will create a folder named models
`mkdir models && cd models`

#### We will create a file named book.js
`vi book.js`

#### We will then copy and paste the code below into ‘book.js’
`var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';
mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = mongoose.model('Book', bookSchema);`

### Step 4 – Access the routes with AngularJS

### In the book directory, we will create a folder named public
`mkdir public && cd public`

#### We will add a file named script.js
`vi script.js`

#### We will copy and paste the Code below (controller configuration defined) into the script.js file.

`var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
  $http( {
    method: 'GET',
    url: '/book'
  }).then(function successCallback(response) {
    $scope.books = response.data;
  }, function errorCallback(response) {
    console.log('Error: ' + response);
  });
  $scope.del_book = function(book) {
    $http( {
      method: 'DELETE',
      url: '/book/:isbn',
      params: {'isbn': book.isbn}
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
  $scope.add_book = function() {
    var body = '{ "name": "' + $scope.Name + 
    '", "isbn": "' + $scope.Isbn +
    '", "author": "' + $scope.Author + 
    '", "pages": "' + $scope.Pages + '" }';
    $http({
      method: 'POST',
      url: '/book',
      data: body
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
});`

In public folder, we will create a file named index.html;
`vi index.html`

#### We will copy and paste the code below into index.html file.
`<!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div>
      <table>
        <tr>
          <td>Name:</td>
          <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
          <td>Isbn:</td>
          <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
          <td>Author:</td>
          <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
          <td>Pages:</td>
          <td><input type="number" ng-model="Pages"></td>
        </tr>
      </table>
      <button ng-click="add_book()">Add</button>
    </div>
    <hr>
    <div>
      <table>
        <tr>
          <th>Name</th>
          <th>Isbn</th>
          <th>Author</th>
          <th>Pages</th>

        </tr>
        <tr ng-repeat="book in books">
          <td>{{book.name}}</td>
          <td>{{book.isbn}}</td>
          <td>{{book.author}}</td>
          <td>{{book.pages}}</td>

          <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
        </tr>
      </table>
    </div>
  </body>
</html>`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/7c99fb66-0f6f-465e-a185-022395722961)


#### In the Books directory, we will Start the server by running this command:
`node server.js`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/286b4600-0e66-41cb-8836-81a21aefd0bd)


#### The server is now up and running, we can connect it via port 3300. You can launch a separate Putty or SSH console to test what curl command returns locally.
`curl -s http://16.171.138.206:3300`

#### And the Web Book Register Application is ready:

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/d956a49e-0736-42d0-8483-ac8b88b7ace3)






















