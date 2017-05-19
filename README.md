# Angular CLI + Express server Setup

1) Install Angular CLI
2) ng new [Project Name]
3) open Project folder
4) ng Serve -
	Check running angular Base Project on http://localhost://4200

# Adding Express Server
5) ng build -
	This command build a dist folder on root that you can fild index.html

6) Install Express dependencies -
	npm install --save express body-parser

7) Create server folder and server.js on root in angular project

8) Paste following code in server.js

# Server.js

// Get dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const bodyParser = require('body-parser');

// Get our API routes
const api = require('./server/routes/api');

const app = express();

// Parsers for POST data
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));

// Point static path to dist
app.use(express.static(path.join(__dirname, 'dist')));

// Set our api routes
app.use('/api', api);

// Catch all other routes and return the index file
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, 'dist/index.html'));
});

/**
 * Get port from environment and store in Express.
 */
const port = process.env.PORT || '3000';
app.set('port', port);

/**
 * Create HTTP server.
 */
const server = http.createServer(app);

/**
 * Listen on provided port, on all network interfaces.
 */
server.listen(port, () => console.log(`API running on localhost:${port}`));


9) Create routes folder under server folder which is on root and create app.js into route folder
	paste the following code into it

# app.js

const express = require('express');
const router = express.Router();

/* GET api listing. */
router.get('/', (req, res) => {
  res.send('api works');
});

module.exports = router;

10) build the project using command ng build

11) run node server - Check your app on browser localhost://3000 it shows app works!, and localhost://3000/api shows api works which is showing output of api.js

Pull this branch of the same code

Cheers :)