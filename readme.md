# Node.js Web Application
The following are instructions on creating a simple web application and deploying it to a remote server. The application will be built on Node.js with Express, and hosted on Heroku. 

## Pre-requisites
You will need the following installed on your local machine:
1. [NodeJS and NPM](http://treehouse.github.io/installation-guides/)
2. Terminal program such as [Git Bash](https://gitforwindows.org/), [Hyper](https://hyper.is/)
3. Code editor program such as [Sublime](https://www.sublimetext.com/download), [Atom](https://atom.io/)
4. [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

## App development
### Initiating the Express application
1. In your local machine, create a directory and change your active directory to it
```
mkdir portfolio-app
cd portfolio-app
```
2. Initiate the app using `npm init -y`
3. Install express to the app using `npm install express --save`

### Create the application file
1. Create an app.js file
```
touch app.js
```
2. Open the app.js file in a code editor program and create the Express server 
```
const express = require('express');
const app = express();
app.listen(3000, function()
  {console.log("Server started on port 3000");}
);
```
3. Test it by running the app using `node app.js` in your terminal and access localhost:3000 on your browser, you should see 'Cannot GET /'
4. Press Ctrl + C in the terminal to stop running the app

### Write Express routes in application file
1. Add a get route to the app.js file 

```
const express = require('express');
const app = express();
app.get("/", function(req, res){
  res.send('Hello world');
});
app.listen(3000, function()
  {console.log("Server started on port 3000");}
);
```
2. Run the app again using `node app.js` and access localhost:3000, you should see 'Hello world' now
3. Press Ctrl + C in the terminal to stop running the app

### Install some useful dependencies to the app
1. Install [nodemon](https://www.npmjs.com/package/nodemon) so that the server restarts automatically when you make changes to the files `npm install nodemon`
2. Install a template engine that can be used to serve page content such as [EJS](https://www.npmjs.com/package/ejs) `npm install ejs` 

### Configure the app to use EJS templates
Add this line of code in your app.js file:
```
app.set("view engine", "ejs");
```

### Create a page template
1. In your terminal, create a new directory called *views* in the portfolio-app directory and change directory into it
```
mkdir views
cd views
```
2. Create a new page template using `touch home.ejs`
3. Go back to the root directory /portfolio-app `cd ..`
4. In your code editor, open up home.ejs and insert basic HTML codes for a page
```
<html>
  <head>
    <title>Portfolio App</title>
  </head>
  <body>
    <p>This is a test page!</p>
  </body>
</html>
```

### Update application file to serve page template
1. In your code editor, open up app.js and alter the get route to serve the page template you created
```
app.get("/", function(req, res){
  res.render('home');
});
```
2. In your terminal, run the app using `node app.js` or `nodemon app.js` if you installed nodemon package
3. Access localhost:3000 on your browser and it should display a page based on the HTML codes you inserted in the page template
4. Press Ctrl + C in the terminal to stop running the app if you used `node app.js` to start the app

### Deploy application to Heroku
1. Make changes to the listen method in your app.js file since you cannot define a port number when using Heroku 
```
const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log('This app is running on port' + port);
});
```
2. Create a PROC file in the project directory using `touch Procfile`. This file will contain the commands that will be executed by the server to run the application.
3. Edit Procfile in your code editor and add this line
```
web: node app.js
```
4. Create a local git repository in your project directory (e.g. /portfolio-app) and commit the files
```
git init 
git add .
git commit -m “first commit”
```
5. In your terminal, login to heroku using `heroku login`
6. Create a heroku app using `heroku create`
7. Push the application files in your local git repository to heroku using `git push heroku master`
8. Your web application is now accessible on a public URL i.e. https://stark-escarpment-62732.herokuapp.com/ & https://serene-reaches-92431.herokuapp.com/

## Project directory structure
Your final project directory should have the following structure:
```
/portfolio-app
    |__ /node_modules
    |__ /views            
         |__ home.ejs
    |__ app.js
    |__ Procfile
    |__ package.json
    |__ package-lock.json

```
