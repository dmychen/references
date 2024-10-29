# Backend  

Database interactions, account logins or purchases happen in the backend.  

### Application Server  

A server is a computer program that supports other programs and users  

It receives requests and performs actions.  

> Step 1: Website asks server "get user info for MR CRUZ"  
> Step 2: Server queries a database  
> Step 3: Server returns data to website  

### API  

Receives requests to our application server. Only a backend.  

Attached to our server, receives requests and processes it.  

Different types of requests: `GET`, `POST` `PUT`, `PATCH`, `DELETE`, and more.  

> GET request to get user info from a database  
> POST request to add new user info  
> ...etc...  

Each API service is called a route.  

We can make our own APIs, or use other people's APIs. This is useful to access databases outside of our application, etc...  

> There are weather APIs, twitter APIs, map APIs, chatgpt APIs, etc...  

## ExpressJS

Backend web application javascript framework.  

Used to build APIs and routes to our APIs.  

> React (Frontend) <---> Node.js (middle) and ExpressJS (backend)  

### Initializing a Project  

	mkdir express-app
	cd express-app
	npm init
	npm install -save express body-parser
	npm start
	
Then we can create an `index.js` file, linking it with `"start": "node ./index.js",` in our package.json.  


### Routes

We create a get route with:  

	route.get('name-here', (req, res) => {
		// stuff in here
	});
	
### Axios  

`npm install express axios` Installs axios!  

Axios is an express library that allows us to use other people's APIs.  

### Node Mailer

`npm install nodemailer` Install nodemailer!  


### Postman  

We use postman as a API tester.  

A client to test our APIs, instead of a web browser.  
