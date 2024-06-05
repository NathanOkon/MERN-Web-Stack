## WEB STACK IMPLEMENTATION (MERN) IN AWS

![M1](./Images/M1.png)

**Introduction**

As a DevOps Engineer In training on Steghub, I learned to deploy a `MERN` stack application on AWS. The `MERN` stack is a JavaScript stack designed to make the development process smoother. MERN includes four open-source components: **M**ongoDB, **E**xpress, **R**eact, and **N**ode. These components provide an end-to-end framework for web developers to work in. In this documentation, I will be demonstrating how to successfully deploy a `MERN` stack application on AWS.

# Prerequisites

Before we begin let's make sure you are all set to proceed. Below are the prerequisites for this project:

- [x] **AWS Account**: You need to have an AWS account to begin with. If you don't have one, you can create one [here](https://aws.amazon.com/).

- [x] **Basic Understanding of JavaScript**: You can get up to speed with JavaScript basics [here](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics).

- [x] **Basic Understanding of React**: You can check out this page [here](https://legacy.reactjs.org/tutorial/tutorial.html).
- [x] **Basic Understanding of Node.js**: You can check out this simple intro [here](https://nodejs.dev/learn).
- [x] **Basic Understanding of MongoDB**: You can check out this simple intro [here](https://www.mongodb.com/company/what-is-mongodb).

## Task - 101 Prepare MERN Pre-requisites

Before we can deploy the  `MERN` stack application on AWS, we need to prepare the following prerequisites:

- [x] **Set up AWS Account**.
- [x] **Create an Ubuntu EC2 Instance**
- [x] **Update firewall rules**


Our EC2 Instance is now ready for the next steps for developing and deploying the TO-DO web up on the MERN stack.
The TO-DO web application will have a backend infrastructure using Node.js and Express.js, a frontend using React.js, and a NOSQL database set up using MongoDB. our Ubuntu EC2 instance will be the host for the backend and frontend of the application.
![I2](./Images/W1.png)

For the next steps, let's configure our Backend.

## Task - 102 Configure Backend
in this task, we will be configuring the backend of our TO-DO web application. The backend will be set up using Node.js and Express.js. We will also set up a NOSQL database using MongoDB.

### Install Node.js
`Node.js` will be used to run the backend logic for our TO-DO web app written in JavaScript. [Node.js](https://nodejs.org/en) uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. It is perfect for data-intensive real-time applications that run across distributed devices.

To install Node.js, run the following commands:

```bash
sudo apt update && sudo apt upgrade -y
```
![W2](./Images/W2.png)


Add repository for Node.js package for Ubuntu. Doing so will allow us to install the latest version of Node.js.
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
![W3](./Images/W3.png)

Install the Latest Node.js package for Ubuntu.
```bash
sudo apt-get install -y nodejs
```
![W4](./Images/W4.png)

The above command will install node and [npm](https://www.npmjs.com/), the package manager for Node.js. package managers help developers to install, update, configure, and uninstall code libraries and dependencies.

now let's check the version of Node.js and npm installed.
```bash
node -v
npm -v
```
The output should be the version of Node.js and npm installed.

![W5](./Images/W5.png)

great! Node.js and npm are now installed on our EC2 instance. Next, we will set up the directory structure for the TO-DO app. This helps to keep the codebase organized and maintainable.

### Set up Directory Structure

Create a directory for the TO-DO app.
```bash
mkdir Todo && cd Todo
```
With this command, we created and changed into the Todo directory. Next, we will initialize a new Node.js project in the Todo directory.

### Initialize Node.js Project

I initialized a new Node.js project in the Todo directory using the following command:
```bash
npm init
```

The `npm init` command creates a `package.json` file in the Todo directory. The `package.json` file contains metadata about the project and the dependencies required to run the project. Next, we will install the dependencies required to run the TO-DO app.
![W6](./Images/W6.png)

### Install Dependencies

One of the backend dependencies for our `MERN` web app is the Express.js framework. The development team will use Express.js to define the routes and handle requests from the frontend(we are yet to setup). To install Express.js, run the following command:

```bash
npm install express
```
![I8](./Images/W7.png)

Great! Express.js is now installed in our project. Next up, we will create an index route for the TO-DO app to test if the backend is working as expected.

### Create Index Route

I created an index route in the `index.js` file in the Todo directory. The index route will be used to test if the backend is working as expected. Here is the code for the index route:

```bash
touch index.js
```

Run ls ton confirm that your index.js file is successfully created.
![W8](./Images/W8.png)

Install the dotenv module
```bash
npm install dotenv
```
![W9](./Images/W9.png)

I will then define the index route in the `index.js` file. The index route will return a message to the client when the client makes a request to the route. Here is the code for the index route:

Open index.js file
```bash
vim index.js
```

```javascript
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
  next();
});

app.use((req, res, next) => {
  res.send('Welcome to Express');
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```
![W9](./Images/W9.png)

The code above defines an index route that returns a message to the client(the browser or another server) when the client makes a request to the route. The server listens on port 5000 by default. The [port number](https://www.google.com/search?q=what+are+port+numbers&oq=what+are+port+numbers&aqs=chrome..69i57j0i512l4j0i22i30l5.6222j0j7&sourceid=chrome&ie=UTF-8) can be changed by setting the `PORT` [environment variable.](https://www.geeksforgeeks.org/environment-variables-in-linux-unix/)

Notice how our express app is listening on port number `5000` by default. We need to ensure that our EC2 instance allows traffic on port 5000. We will do this by updating the inbound rules for the EC2 instance. I[ added a custom TCP rule](https://docs.aws.amazon.com/finspace/latest/userguide/step5-config-inbound-rule.html) for port 5000 to allow traffic from all IP addresses(not a particularly strict inbound rule but we'll manage).
![W11](./Images/W11.png)

let's try it out in the browser. Open a browser and navigate to `http://<public-ip>:5000`. You should see the message "Welcome to the TO-DO app powered by MERN stack".

![W12](./Images/W12.png)
Great! The backend is working as expected. Before we do the next steps, let's quickly review what we have done so far.
We are setting up a MERN stack application on AWS. After spinning up an EC2 instance, we installed Node.js and npm. We then set up the directory structure for the TO-DO app and initialized a new Node.js project. We installed the Express.js framework and created an index route to test if the backend is working as expected. The index route returns a message to the client when the client makes a request to the route. We also updated the inbound rules for the EC2 instance to allow traffic on port 5000. The backend is now ready for the next steps.

### ah yes! your very own surprise side quest.

You have earned a quick pause for hydration :) when you return we'll define the routes for the TO-DO app.

<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExd3VuMG0zZ3Q3aHc5aTk3NnM0NjhkMXp4NGZmdjljbGZkMGJuaHh1aSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/63whWnKaTj0Tm/giphy.gif" alt="gif showing cat drinking water" style="width:1000px; padding-top:20px; padding-bottom:50px">


## Task - 103 Define Routes for TO-DO App

Now that the backend is working as expected, let's put on our backend web developer hats and define some simple routes for our TO-DO app. Think of routes as being the different paths that a user can take to interact with the app. The routes will be used to perform [CRUD operations](https://www.freecodecamp.org/news/crud-operations-explained/) on the TO-DO app. CRUD stands for Create, Read, Update, and Delete. The routes we will design will help our users create a new TO-DO item, read all TO-DO items, update a TO-DO item, and delete a TO-DO item.

### Create Routes

we can define routes inside the `index.js` file but that would make the codebase messy and hard to maintain. To keep the codebase organized and maintainable, we will create a new directory called `routes` and define the routes in separate files. Let's create the `routes` directory and define the routes for the TO-DO app.

```bash
mkdir routes && cd routes && touch api.js
```
![W3A](./Images/W13A.png)

inside the `routes` directory, we will create a new file called `api.js` and define the routes for the TO-DO app. Here is the code for the `api.js` file:

```javascript
const express = require('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

});

module.exports = router;
```
![W13](./Images/W13.png)

## Task - 104 Model TO-DO Items

We will use the routes defined inside the `api.js` in a moment. For now, we need to model the real-world idea of a TO-DO item. You can think of modeling as us defining a blueprint in Javasript for spawning TO-DO objects. The model will define the structure of a TO-DO item, giving it properties, and methods to interact with the TO-DO item.


| Field        | Type   | Description                              |
|--------------|--------|------------------------------------------|
| id           | String | A unique identifier for the TO-DO item.  |
| action       | String | The title of the TO-DO item.             |
| description  | String | A detailed description of the TO-DO item.|
| status       | String | The status of the TO-DO item.            |
| created_at   | Date   | The date and time when the TO-DO item was created. |
| updated_at   | Date   | The date and time when the TO-DO item was last updated. |


when these TO-DO objects are created by the user we need a way to persist them for retrieval later.(we don't want to lose our TO-DO items when the server is restarted). We will use a NOSQL database to store the TO-DO items. at the risk of sounding repetitive, we will use MongoDB as the NOSQL database.

### Set up NoSQL Database

We need to install a node.js package called `mongoose` to interact with MongoDB. Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides a straightforward, schema-based solution to model the application data. To install mongoose, run the following command:

```bash
npm install mongoose
```
![W14](./Images/W14.png)

### Define TO-DO Models

We will define the TO-DO model in a new file called `todo.js` inside the `models` directory. Let's create the `models` directory and define the TO-DO model.

```bash
mkdir models && cd models && touch todo.js
```
![NW15](./Images/W15.png)

Inside the `todo.js` file, we will define the TO-DO model. Here is the code for the `todo.js` file:

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// Create schema for todo
const TodoSchema = new Schema({
  action: {
    type: String,
    required: [true, 'The todo text field is required']
  }
});

// Create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;
```
![W16](./Images/W16.png)

### Integrate Routes and Models

Now that we have the blueprint for creating and storing todo items via `models/todo.js` and the half-baked API request endpoints defined in the `api.js`, it's time to fully implement the CRUD operations defined in the `api.js` file. We will use the `mongoose` package to interact with the MongoDB database. Let's integrate the routes and models.

```javascript
const express = require('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {
  // This will return all the data, exposing only the id and action field to the client
  Todo.find({}, 'action')
    .then(data => res.json(data))
    .catch(next);
});

router.post('/todos', (req, res, next) => {
  if (req.body.action) {
    Todo.create(req.body)
      .then(data => res.json(data))
      .catch(next);
  } else {
    res.json({
      error: "The input field is empty"
    });
  }
});

router.delete('/todos/:id', (req, res, next) => {
  Todo.findOneAndDelete({"_id": req.params.id})
    .then(data => res.json(data))
    .catch(next);
});

module.exports = router;
```
![W17](./Images/W17.png)
At this point our backend is almost ready. We have all the API endpoints the client side will need to interact with the backend. We have also defined the TO-DO model to create the TO-DO items. The next step is to connect the backend to the MongoDB database. 

### MongoDB Database

We will need a database where we will store our data. For this we will make use of mLab. mLab provides MonogoDB Database as a server solution(DBaas), so to make life easy, we will need to sign up for a shared cluster free account, which is ideal for our use case.
![W18](./Images/W18.png)

**Create a file in your Todo directory and name it . env**
```bash
touch .env
vi .env
```

**Add the connection string to access the database in it, just as below.

```bash
DB = 'mongodb+srv://nathanieldavid06:zeWDCw6CcRPTMiKJ@cluster0.r7cm5fo.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0'
```
![W19](./Images/W19.png)

**Update the index.js to reflect the use of .env so that Node.js can connect to the database.**

```bash
vim index.js
```

**Delete existing content in the file, and update it with the entire code below:**
```bash
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

// Connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log(`Database connected successfully`))
  .catch(err => console.log(err));

// Since mongoose promise is deprecated, we override it with Node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
  next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
  console.log(err);
  next();
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```
![W20](./Images/W20.png)

Using environment variables to store information is considered more secure and best practice to separate configuration and secret data from the application, instead of writing connection strings directly inside the index.js application file.

**Start your server using the command**
```bash
node index.js
```
![W21](./Images/W21.png)

There was a deprecation warning as diplayed in the image above.
To silent this warning, __{ useNewUrlParser: true, useUnifiedTopology: true }__ was removed from the code.


## Testing Backend Code without Frontend using RESTful API

Postman was used to test the backend code.
The endpoints were tested. For the endpoints that require body, JSON was sent back with the necessary fields since it’s what was set up in the code.

__1.__ __Open Postman and Set the header__

```bash
http://13.60.82.188:5000/api/todos
```
![W22](./Images/W22.png)

### Create POST requests to the API

![Post request](./Images/W23.png)
![Post request](./Images/W24.png)
![Post request](./Images/W25.png)
![Post request](./Images/W26.png)

### Check Database Collections

![DB CollectiomW27](./Images/W27.png)


### Make a GET requests to the API

This request retrieves all existing records from our To-Do application (backend requests these records from the database and sends us back as a response to GET request).

![Get request](./Images/W28.png)


## Step 2 - Frontend Creation

It is time to create a user interface for a Web client (browser) to interact with the application via API

__1.__ __In the same root directory as your backend code, which is the Todo directory, run:__

```bash
npx create-react-app client
```
![React](./Images/W29.png)

This created a new folder in the Todo directory called client, where all the react code was added.

### Running a React App

Before testing the react app, the following dependencies needs to be installed in the project root directory.

- __Install concurrently__. It is used to run more than one command simultaneously from the same terminal window.
```bash
npm install concurrently --save-dev
```
![Concurrent](./Images/W30.png)


- __Install nodemon__. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
```bash
npm install nodemon --save-dev
```
![Nodemon](./Images/W31.png)


- In Todo folder open the package.json file, change the highlighted part of the below screenshot and replace with the code below:
```bash
"scripts": {
  "start": "node index.js",
  "start-watch": "nodemon index.js",
  "dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
}
```

### Configure Proxy In package.json

- Change directory to “client”
```bash
cd client
```

- Open the package.json file
```bash
vim package.json
```
![Package](./Images/W32.png)

Add the key value pair in the package.json file
```bash
“proxy”: “http://localhost:5000”
```
![Proxy](./Images/W33.png)

The whole purpose of adding the proxy configuration above is to make it possible to access the application directly from the browser by simply calling the server url like
http://locathost:5000 rather than always including the entire path like http://localhost:5000/api/todos

Ensure you are inside the Todo directory, and simply do:
```bash
npm run dev
```
![W34](./Images/W34.png)
The app opened and started running on localhost:3000

__Note__: In order to access the application from the internet, TCP port 3000 had been opened on EC2.


## Creating React Components

One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For the Todo app, there are two stateful components and one stateless component. From Todo directory, run:

```bash
cd client
```

Move to the “src” directory
```bash
cd src
```

__2.__ __Inside your src folder, create another folder called “components”__

```bash
mkdir components
```
Move into the components directory
```bash
cd components
```
![Component](./Images/W35.png)

__3.__ __Inside the ‘components’ directory create three files “Input.js”, “ListTodo.js” and “Todo.js”.__
```bash
touch Input.js ListTodo.js Todo.js
```
![Component files](./Images/W36.png)

#### Open Input.js file
```bash
vim Input.js
```
Paste in the following:

```
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {
  state = {
    action: ""
  }

  handleChange = (event) => {
    this.setState({ action: event.target.value });
  }

  addTodo = () => {
    const task = { action: this.state.action };

    if (task.action && task.action.length > 0) {
      axios.post('/api/todos', task)
        .then(res => {
          if (res.data) {
            this.props.getTodos();
            this.setState({ action: "" });
          }
        })
        .catch(err => console.log(err));
    } else {
      console.log('Input field required');
    }
  }

  render() {
    let { action } = this.state;
    return (
      <div>
        <input type="text" onChange={this.handleChange} value={action} />
        <button onClick={this.addTodo}>add todo</button>
      </div>
    );
  }
}

export default Input;
```
![Input](./Images/W37.png)

In oder to make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios.

Move to the client folder
```bash
cd ../..
```
__Install Axios__
```bash
npm install axios
```
![](./Images/W38.png)

#### Go to components directory
```bash
cd src/components
```

#### After that open the ListTodo.js

```bash
vim ListTodo.js
```
Copy and paste the following code:

```bash
import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {
  return (
    <ul>
      {
        todos && todos.length > 0 ? (
          todos.map(todo => {
            return (
              <li key={todo._id} onClick={() => deleteTodo(todo._id)}>
                {todo.action}
              </li>
            );
          })
        ) : (
          <li>No todo(s) left</li>
        )
      }
    </ul>
  );
}

export default ListTodo;
```
![Todo list](./Images/W39.png)

#### Then in the Todo.js file, write the following code

```bash
vim Todo.js
```

```bash
import React, { Component } from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {
  state = {
    todos: []
  }

  componentDidMount() {
    this.getTodos();
  }

  getTodos = () => {
    axios.get('/api/todos')
      .then(res => {
        if (res.data) {
          this.setState({
            todos: res.data
          });
        }
      })
      .catch(err => console.log(err));
  }

  deleteTodo = (id) => {
    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if (res.data) {
          this.getTodos();
        }
      })
      .catch(err => console.log(err));
  }

  render() {
    let { todos } = this.state;
    return (
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos} />
        <ListTodo todos={todos} deleteTodo={this.deleteTodo} />
      </div>
    );
  }
}

export default Todo;
```
![Todo](./Images/W40.png)

__We need to make a little adjustment to our react code. Delete the logo and adjust our App.js to look like this__

### Move to src folder
```bash
cd ..
```

Ensure to be in the src folder and run:
```bash
vim App.js
```

#### Copy and paste the following code

```bash
import React from 'react';
import Todo from './components/Todo';
import './App.css';

const App = () => {
  return (
    <div className="App">
      <Todo />
    </div>
  );
}

export default App;

```
![Appjs](./Images/W41.png)

####  In the src directory, open the App.css

```bash
vim App.css
```

Paste the following code into it

```bash
.App {
  text-align: center;
  font-size: calc(10px + 2vmin);
  width: 60%;
  margin-left: auto;
  margin-right: auto;
}

input {
  height: 40px;
  width: 50%;
  border: none;
  border-bottom: 2px #101113 solid;
  background: none;
  font-size: 1.5rem;
  color: #787a80;
}

input:focus {
  outline: none;
}

button {
  width: 25%;
  height: 45px;
  border: none;
  margin-left: 10px;
  font-size: 25px;
  background: #101113;
  border-radius: 5px;
  color: #787a80;
  cursor: pointer;
}

button:focus {
  outline: none;
}

ul {
  list-style: none;
  text-align: left;
  padding: 15px;
  background: #171a1f;
  border-radius: 5px;
}

li {
  padding: 15px;
  font-size: 1.5rem;
  margin-bottom: 15px;
  background: #282c34;
  border-radius: 5px;
  overflow-wrap: break-word;
  cursor: pointer;
}

@media only screen and (min-width: 300px) {
  .App {
    width: 80%;
  }

  input {
    width: 100%;
  }

  button {
    width: 100%;
    margin-top: 15px;
    margin-left: 0;
  }
}

@media only screen and (min-width: 640px) {
  .App {
    width: 60%;
  }

  input {
    width: 50%;
  }

  button {
    width: 30%;
    margin-left: 10px;
    margin-top: 0;
  }
}

```
![App css](./Images/W42.png)

#### In the src directory, open the index.css

```bash
vim index.css
```
![src](./Images/W43.png)


#### Copy and paste the code below:

```bash
body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  background-color: #282c34;
  color: #787a80;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New", monospace;
}
```
![index css](./Images/W44.png)

#### Go to the Todo directory
```bash
cd ../..
```

Run:
```bash
npm run dev
```
![dev](./Images/W45.png)

At this point, the To-Do app is ready and fully functional with the functionality discussed earlier: Creating a task, deleting a task, and viewing all the tasks.

__The client can now be viewed in the browser__

![Todo web](./Images/46.png)

__Add some todos via the browser .__

![Todos](./Images/46.png)

__Check them on the MongoDB database__

![Todo](./Images/47.png)

### Conclusion

By following this documentation and leveraging the provided resources, one is well-equipped to build and deploy full-fledged web applications utilizing the MERN stack.





.

## Congratulations on making it this far 🥇
<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExN2xzbmRvNXczdWhtc3luZXRqMmF1ZzVyMXFhaGp6MTU3cW5vcnQ3OSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/KAw0oBpBXAQbkVS4yG/giphy.gif" style="width:1000px;" >






## Conclusion

In this project, we set up a MERN stack application development environment on AWS. We created a TO-DO app using the MERN stack. We set up the backend using Node.js and Express.js. We defined the routes for the TO-DO app and modeled the TO-DO items. 
