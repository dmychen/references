# DevX Intern Workshops

## React  

Learning how to use the basics of React.  

`export default`  

`index.js` Bridge between components in `App.js`and the web browser.  

`import { library } from 'source'` Imports libraries.  

> `import { StrictMode } from 'react'`  
> import { createRoot } from 'react-dom/client';  

### JSX

In React, rendering logic and markup both live inside components. Most often, React is used in combination with **JSX** in order to achieve this. A  **jsx element** is a combination of javascript code and html tags.  

When returning from a functino in JSX, we must return a single root html element. This is because the HTML in JSX is transformed into a plain Javascript object under the hood, and we can only return one object from a function. 
Often we wrap JSX tags in a `<div> </div>` tag if we need to return multiple tags together. We can also use `<> </>`, which is a [fragment](https://react.dev/reference/react/Fragment).  

In JSX, most HTML and SVG attributes are written in camelCase which correspond to [DOM properties](https://developer.mozilla.org/en-US/docs/Web/API/Element/className). Here is a [list of common props](https://react.dev/reference/react-dom/components/common).

### Rendering Lists

We use [javascript array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) to manipulate arrays of data.  

We can filter and transform our arrays of data into an array of components using React's `map()` and `filter()`.  

`map()` maps an array to corresponding react components.  

`filter()` Takes a list and filters out what we don't want.  

We need to give each item a **key**, which uniquely identified it within that array. A key could be an ID from whatever database is storing the data, or for local data it could be an incrementing counter like `crypto.randomUUIID()`. Keys must not change, don't generate them while rendering.  

	originalList = [{
		id: 0,
		value: 'something',
		somethingElse: 'idk'
	}, {
		id: 1,
		value: 'not the same',
		somethingElse: 'boo!'
	}]
	
	
	const newList = originalList.filter(item => 
		item.value === 'something'
	);
	
    const componentList = newList.map(item => 
   	<li key={list.id}>
		<p> 
		How we want the data in item to be transformed into a component.
		</p>
		<button> Remove {item.value} </button>
	</li>
	);

If we want each item to render into several different DOM nodes, we need to group everything into a single `<div>` or [explicit fragment](https://react.dev/reference/react/Fragment#rendering-a-list-of-fragments) `<Fragment>`.  


## Backend  

Database interactions, account logins or purchases happen in the backend.  

#### Application Server  

A server is a computer program that supports other programs and users  

It receives requests and performs actions.  

> Step 1: Website asks server "get user info for MR CRUZ"  
> Step 2: Server queries a database  
> Step 3: Server returns data to website  

#### API  

Receives requests to our application server. Only a backend.  

Attached to our server, receives requests and processes it.  

Different types of requests: `GET`, `POST` `PUT`, `PATCH`, `DELETE`, and more.  

> GET request to get user info from a database  
> POST request to add new user info  
> ...etc...  

Each API service is called a route.  

We can make our own APIs, or use other people's APIs. This is useful to access databases outside of our application, etc...  

> There are weather APIs, twitter APIs, map APIs, chatgpt APIs, etc...  

### ExpressJS

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


#### Routes

We create a get route with:  


	route.get('name-here', (req, res) => {
		// stuff in here
	});
	
#### Axios  

`npm install express axios` Installs axios!  

Axios is an express library that allows us to use other people's APIs.  

### Node Mailer

`npm install nodemailer` Install nodemailer!  


#### Postman  

We use postman as a API tester.  

A client to test our APIs, instead of a web browser.  

## Databases

Stores all data for a web app.  

-  Accessed via the application server (API)  
- Data is often structured (tables, columns, rows)  
- Stores: user info, login credentials, etc...  

Types of databases:  
- Spreadsheets (csv): Google sheets, excel.  
  - Useful for humans, not useful for programs.  
- Relational databases (sql): MySQL, postgreSQL  
  - Structured data with fixed schema.  
  - Commonly used, pretty scalable.  
- Non-relational databases (no sql): MongoDB
  - Semi-structured data with flexible schema.  
  
Structure of SQL:  
- Organized in columns (ie: ID, Name, Address), and rows (1, 2, 3...)  

### SQL  

Allows us to write scripts to access and manipulate our database.  

- `SELECT * FROM users;` Retrieve information for all users.  

> `*` represents 'all'  

- `SELECT * FROM users WHERE user_id = 1;` Retrieve from specific user.  

- `UPDATE users SET email = 'test@gmail.com' WHERE user_id = 1;` Update information.  

- `DELETE FROM users ...` etc...

#### MySQL  

A database management system, that uses SQL.  

Setup: Once a connection is created...  



## Full Stack

The term tech stack refers to the collection of languages and frameworks we use to create our applications.  

We've been using React + Node + Express + MySQL.  


## App Deployment

How can we make our web apps accessible on the internet. Building, testing, and deploying to the cloud.

**CI/CD**: Continuous integration and deployment.  

How do we turn code into a live application? 

> Application Code ->   
> Source (Git) -> Build ->  
> Test (Unit test/integration test) ->   
> Deploy (staging, QA, production)  

### Enterprise CI/CD

Cloud infrastructure -> Allows us to deploy our applications  
- Microsoft Azure, AWS, Google Cloud  
- Used by companies to host frontend, backend, database, etc...  

> Containerization: Kubernetes, Openshift, Docker.  

### Github pages

Allows free deployment for static websites (ie React apps)  
- Automatic deployment through Github.  
- Only for frontend stuff.  
- Backend deployment must be done with another service.  
  - use Heroku or some other cloud infrastructure service.  
  

## Project Management  

Organization of work. Very common to use agile project management, where we work in sprints.  

### The Agile Workflow  

**Sprints**: organize tasks based on sprints, which last a few weeks.  
- Sprint planning at the beginning of the sprint.  
- Sprint review at the end of each sprint.  
- Sprint retrospective.  

**Daily scrums**: standup meetings.  

> Product backlog ->  
> Sprint backlog ->  
> Sprint (planning - implementation - review (+ daily scrums) - retrospective) ->  
> Completed Project.  

**Scrumboard**: a taskboard.  
- Each member assigned tasks for different projects or separate features on the same project.  
- tasks to complete are often called issues or stories.  





