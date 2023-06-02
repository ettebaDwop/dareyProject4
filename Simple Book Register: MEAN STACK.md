# A simple Book Register web form using MEAN stack.

MEAN Stack is a combination of following components:
- MongoDB (Document database) – Stores and allows to retrieve data.
- Express (Back-end application framework) – Makes requests to Database for Reads and Writes.
- Angular (Front-end application framework) – Handles Client and Server Requests
- Node.js (JavaScript runtime environment) – Accepts requests and displays results to end user

The steps involved here are as follows:
1. Install NodeJs
2. Install MongoDB
3. Install Express and set up routes to the server
4. Access the routes with AngularJS


#### Step 1 Install NodeJs
TO install NodeJS, run the following commands:

` sudo apt update && apt upgrade`

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.lis

```

Add certificates

```
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
Install NodeJS

` sudo apt install -y nodejs`

#### Step 2 Install MongoDB

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.lis
```

` sudo apt install -y mongodb`

Running the code above brings up errors due to version compattibility and deprecation of some packages. 

![image](https://github.com/ettebaDwop/dareyProject4/assets/7973831/e98f3543-9beb-47cf-859b-4b1d20f45e18)

The error above imples that, MongoDb has no official build for ubuntu 22.04 at the moment. Thus, Ubuntu 22.04 has upgraded libssl to 3 and does not propose libssl1.1

To solve this problem, we will force the installation of libssl1.1 by adding the ubuntu 20.04 source:

` echo "deb http://security.ubuntu.com/ubuntu focal-security main" | sudo tee /etc/apt/sources.list.d/focal-security.list`

Then run the update command:

` sudo apt-get update`

and install libss11.1

` sudo apt-get install libssl1.1 `  

Re-install MongoDb

` Sudo apt-get install -y mongodb-org`

Delete the file created in line 56.

` sudo rm /etc/apt/sources.list.d/focal-security.list`

Start and enable  Mongodb

` sudo systemctl start mongod `

` sudo systemctl enable mongod`

![image](https://github.com/ettebaDwop/dareyProject4/assets/7973831/5decc155-50d6-405a-899e-b36be733e472)

Verify that the service is up and running by checking the system status

` sudo systemctl status mongodb`

![image](https://github.com/ettebaDwop/dareyProject4/assets/7973831/60253d29-6afe-4647-a120-6fd6f0f2c945)

Install npm – Node package manager.

` sudo apt install -y npm`

Install body-parser package

We need ‘body-parser’ package to help us process JSON files passed in requests to the server.

` sudo npm install body-parser`

![image](https://github.com/ettebaDwop/dareyProject4/assets/7973831/89b59021-04c7-4338-879c-a3d3b6beb6cf)

Create a folder named ‘Books’ and change directory into the folder

` mkdir Books && cd Books`

While in the Books directory, initialize npm 

`npm init`

Add a file to it named server.js

`vi server.js`

Enter the server code into this file to look like so:

![Screenshot (265)](https://github.com/ettebaDwop/dareyProject4/assets/7973831/95048a1b-4ac5-48cc-aaf0-48c1ce166727)

#### Step 3 Install Express and set up routes to the server
Express would be installed using the Mongoose package

` sudo npm install express mongoose`

In ‘Books’ folder, create a folder named apps

` mkdir apps && cd apps`

Edit the apps.js file to look like this:

` vi routes.js`

![Screenshot (267)](https://github.com/ettebaDwop/dareyProject4/assets/7973831/729b0f52-fdff-4ee1-9ae6-01ae362ba42f)

In the ‘apps’ folder, create a folder named models, change directory to the models directory and create / open a new file called book.js

` mkdir models && cd models && vi book.js`

The book.js file contents should look like this:

```
var mongoose = require('mongoose');
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
module.exports = mongoose.model('Book', bookSchema);

```
![image](https://github.com/ettebaDwop/dareyProject4/assets/7973831/e0977bb6-4f4f-4b7e-a499-feeab48e6aa4)

#### Step 4 Access the routes with AngularJS
Change the directory to Books

cd ..

Create a folder named public and add a file named script.js

` mkdir public && cd public && vi script.js`

Paste the following code in the script.js file

```
var app = angular.module('myApp', []);
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
});
```

Run the following commands to change directory back to Books folder and in the public folder, create a file named index.html;

```
cd ..
vi index.html
```

Paste the html code below into index.html file.

```
<!doctype html>
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
</html>
```


Change the directory back up to Books and start the server by running these commands:

```
cd ..
node server.js
```

![image](https://github.com/ettebaDwop/dareyProject4/assets/7973831/526a8119-bf77-4f4b-ae55-dbe139db008e)
