## AWS MERN WEB STACK IMPLEMENTATION

 This project shows how to implement a web solution on MERN stack in AWS Cloud

 MERN stands for (MongoDB, ExpressJS, ReactJS, Node.js,)

---
Creating EC2 Instance

---

We log on to AWS Cloud Services and create an EC2 Ubuntu Instance. When creating an instance, choose keypair authentication downloaded to local system.

![AWS Instance](./Images/Aws%20instance.PNG)

## ................Backend Configuration.............

Update and Upgrade Ubuntu VM

**`sudo apt update && sudo apt upgrade -y`**

![Update and Upgrade](./Images/Update%20and%20Upgrade.PNG)

Lets get the location of Node.js software from Ubuntu repositories.

**`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`**

## **Install Node.js on the server**

Install Node.js with the command below

**`sudo apt-get install -y nodejs`**

![Nodejs install](./Images/Install%20nodejs.PNG)

**Note: The command above installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.**


Verify the node installation with the command below

**`node -v`**

![Node -v](./Images/node%20-v.PNG)


Verify the node installation with the command below

**`npm -v`**

![Npm -v](./Images/mpm%20-v.PNG)


## **Application Code Setup**

Create a new directory for your To-Do project:

**`mkdir Todo`**

Run the command below to verify that the Todo directory is created with ls command

**`ls`**

Inside the **Todo** directory we will instantiate our project using `npm init`. This enables javascript to install packages useful for spinning up our application.


![npm init](./Images/npm%20init.PNG)

Press Enter several times to accept default values, then accept to write out the package.json file by typing **yes**

Run the command ls to confirm that you have package.json file created.



## ................INSTALL EXPRESSJS................

Install ExpressJS

**`npm install express`**


![npm install express](./Images/install%20express.PNG)

Create a file index.js with te command below

**`touch index.js`**

Install the dotenv module

**`npm install dotenv`**

![install dotenv](./Images/dotenv%20install.PNG)

 
Open the index.js file with the command below

**`vi index.js`**

 
 Type the code below into it and save. Do not get overwhelmed by the code you see. For now, simply paste the code into the file.


```
const express = require('express');
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
});

```

specified to use port 5000 in the code. This will be required later when we go on the browser.

Use :wq to save in vim

Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:

**`node index.js`**

![node index.js](./Images/node%20index.js)

We need to open port 5000 in EC2 Security Groups, like this

![inbound security](./Images/inbound%20security%20group.PNG)

Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:


**`http://<PublicIP-or-PublicDNS>:5000`**

![Welcome To Express](./Images/welcome%20to%20Express.PNG)


## Defining Routes For Our Applications

We will create a routes folder which will contain code pointing to the three main endpoints used in a todo application. This will contain the post,get and delete requests which will be helpful in interacting with our client_side and database via restful apis.

```
mkdir routes

cd routes

touch api.js
```

Open the file with the command below:

**`vi api.js`**

Copy and paste the code below:

```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```

## Creating Models

We will be creating the models directory which will be used to define our database schema. A Schema is a blueprint of how our database will be structured which include other fields which may not be required to be stored in the database.

Inside the `todo` directory, run `npm install mongoose` to install mongoose.

Create a `models` directory and then create a file in it `todo.js` Write the below code inside the todo.js file


![Todo](./Images/todo.PNG)

we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

In Routes directory, open `api.js` with vim api.js, delete the code inside with `:%d` command and paste there code below into it then save and exit


```
const express = require ('express');
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

module.exports = router;
```

