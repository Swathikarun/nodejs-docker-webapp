# Dockerizing a Node.js web app

The goal of this example is to show you how to get a Node.js application into a Docker container.

## Requirements

- [Install Docker](https://docs.docker.com/engine/install/)
- [Install Docker Compose](https://docs.docker.com/compose/install/)
- [Install node.js](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html)

## Prerequisite

- Java script that defines a web app using the Express.js framework

- Package file that describes your app and its dependencies

## Creating a java script

create a app.js file that defines a web app using the Express.js framework

```
const express = require("express");
const http = require("http");

const app = express();

const server = http.createServer(app);

app.get('/', function(req,res){
        res.send("<h1><center>Hello, World! Node Application</h1></center>");
});

server.listen(3000, function(){
        console.log("Server is listening on port: 3000");
});
```

## Initialize the project

 $ npm init
 
##  Install Express web application framework

 $ npm install express --save
 
##  Creating a Dockerfile

 $ vi Dockerfile
 
 ```
 FROM node:10
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
CMD node app.js
EXPOSE 8080
 ```
## Create .dockerignore file

This will prevent your local modules and debug logs from being copied onto your Docker image and possibly overwriting modules installed within your image.

```
node_modules
npm-debug.log
```
## Building the image

```
$ docker build -t swathikarun/helloworld:latest .
```

- Pushing the image to repository

```
$ docker image push swathikarun/helloworld:latest
```
- Pulling the image 

```
 $ docker image pull swathikarun/helloworld:latest
```
## Run the image

```
docker run --name nodeapp -d -it -p 8080:3000 helloworld:1
```

## Provisioning

1.Clone the repository

```
 $ git clone https://github.com/Swathikarun/nodejs-docker-webapp.git > mynodeproject
 
 $ cd mynodeproject
 ```
 
2. Check the syntax

  ```
  $ docker-compose config
  ```

3. Creating the docker container

  ```
  $ docker-compose up -d
  ```
## Test

```
 $ curl -X GET http://13.126.4.39:8080/
```

 This command will output "Hello, World! Node Application"
 
## Result

A simple hello-world application in node.js is created and dockerized.
