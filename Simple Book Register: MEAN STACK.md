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

Verify that the service is up and running by checking the system status

` sudo systemctl status mongodb`

Install npm – Node package manager.

` sudo apt install -y npm`

Install body-parser package

We need ‘body-parser’ package to help us process JSON files passed in requests to the server.

` sudo npm install body-parser`
Create a folder named ‘Books’ and change directory into the folder

` mkdir Books && cd Books`

While in the Books directory, initialize npm project

`npm init`

Add a file to it named server.js

`vi server.js`

Enter code to 

#### Step 3 Install Express and set up routes to the server
#### Step 4 Access the routes with AngularJS
