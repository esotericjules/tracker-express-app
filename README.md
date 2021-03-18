### Express Setup

1. Run `npm init -y` to create package.json file.
2. Install these dependencies: bcrypt express jsonwebtoken mongoose nodemon.
3. Create a src directory.
4. Create an index.js file inside src
   Inside index.js,
   - import express
   - create an app object that represents our entire application which we can associate different route handlers with it.
   - create a handler that takes care of get requests to the root route of the application
     ` app.get("/", (req, res) => {});`
   - set the port the app will listen to.
   - run the app in the terminal in mac with `node src/index.js` or using the script you set up for nodemon.

### MongoDB Setup

1. The mongoose library would be used to work with MongoDB
2. We will use a free hosted copy of MongoDB. `cloud.mongodb.com`. The following steps is performed in `cloud.mongodb.com`

- Login to `cloud.mongodb.com`, navigate to create a cluster
- Select a provider and select a free tier location.
- Click on Create Cluster
- After cluster has been created, click on connect and add your current IP Address. (This is subject to change if your wifi connection changes). If you want to addd a new IP Address, click on the network access menu in the sidebar and add the new IP Address
- Create username and password
- Afterwards click on choose a connection method and choose the option that fits what you want
- copy the string of connection uri and paste it inside index.js (express file) and assign it to a variable. Replace <password> with your password

3. Import mongoose library inside the index.js file and connect the connection uri to it like so `mongoose.connect(mongoUri, {....options})`
4. connect to the mongoose instance
   `mongoose.connection.on('connected', () => {})`
5. lof errors from the connection using
   `mongoose.connection.on("error", (err) => {});`

### Authentication Process

1. inside src create a new direcory called **routes**. Inside routes create authRoutes.js
2. Inside authRoutes.js import express
3. Use express to create a router. A router is an object that allows us to associate some number of route handlers with it. We can then associate it back with our route object inside index.js
4. create a function that handler post request to the _/signup_ route.
5. export the router so it can be used by our application `module.exports = router;`
6. inside index.js import the exported route
   `const authRoutes = require('./routes/authRoutes');`
7. To use the route call the use function inside app object and pass it the route as an argument `app.use(authRoutes);`
8. To test out the post request route handler, use postman

**Handling JSONData**
By default the express API does not know how to handle JSON Data.

- Install body-parser and import it inside index.js. (This will parse the JSON information returned in the request body)
- call the app.use function and pass in the bodyParser to it `app.use(bodyParser.json());` This line of code should be above the authRoutes call.
- test out in postman. Add a body to the request using json and set then content-type header to application/json

### Nodemon

This is used to automatically restart our server anytime we make a change to our code. Add this inside scripts in package.json
` "dev": "nodemon src/index.js"`
Now use `npm run dev` when you want to start your server
