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

