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
Running the code above brings up errors due to version compattibility and deprecation of some packages. 
To solve this problem ......

` sudo apt install -y mongodb`

` sudo service mongodb start`

Verify that the service is up and running

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
