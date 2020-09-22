# Routing

* *Routing* refers to how an application's endpoints respond to client requests
    - app.get() for GET requests
    - app.post() for POST requests
- basic route example:
```
var express = require('express')
var app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', function (req, res) {
  res.send('hello world')
})
```

## Route methods

* derived from one of the HTTP methodsw and is attached to an instance of the express class
- example:
```
// GET method route
app.get('/', function (req, res) {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', function (req, res) {
  res.send('POST request to the homepage')
})
```

## Route paths
* define the endpoints at which request can be made
- examples: 
```
app.get('/', function (req, res) {
  res.send('root')
})
```
```
app.get('/about', function (req, res) {
  res.send('about')
})
```
* **Route parameters**
- named URL segments that are used to capture the values specified at their position in the URL

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```
```
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params)
})
```
## Route handlers
* you can provide multiple callback functions that behave like middleware to handle a request

- single callback function can handle a route:
```
app.get('/example/a', function (req, res) {
  res.send('Hello from A!')
})
```
- more than one callback function can handle a route:
```
app.get('/example/b', function (req, res, next) {
  console.log('the response will be sent by the next function ...')
  next()
}, function (req, res) {
  res.send('Hello from B!')
})
```
- an array of callback functions can handle a route:
```
var cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

var cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

var cb2 = function (req, res) {
  res.send('Hello from C!')
}

app.get('/example/c', [cb0, cb1, cb2])
```
- a combination of independent functions and arrays of functions can handle a route:
```
var cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

var cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/d', [cb0, cb1], function (req, res, next) {
  console.log('the response will be sent by the next function ...')
  next()
}, function (req, res) {
  res.send('Hello from D!')
})
```
# Response methods
* methods on a response object (res) can send a response to the client and terminate in the request-response cycle.  Following table shows these methods

- res.download()	Prompt a file to be downloaded.
- res.end()	End the response process.
- res.json()	Send a JSON response.
- res.jsonp()	Send a JSON response with JSONP support.
- res.redirect()	Redirect a request.
- res.render()	Render a view template.
- res.send()	Send a response of various types.
- res.sendFile()	Send a file as an octet stream.
- res.sendStatus()	Set the response status code and send its string          representation as the response body.

## app.route()
* you can create chaiable route handlers for a route path by using app.route()
- example:
```
app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  })
```
## express.Router
* use the express.Touter class to create modular mountable route handlers
- example:
```
var express = require('express')
var router = express.Router()

// middleware that is specific to this router
router.use(function timeLog (req, res, next) {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page')
})
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds')
})

module.exports = router
```

# Supertest
* This is a github to supertest
<https://github.com/visionmedia/supertest>
- helps for testing with applications
- npm i supertest
- require at top of files to include supertest
- its pretty sweet

# Using Middleware
* **Middleware** functions are functions that have access to the req and res objects and the next middleware fucntion in the apps req-res cycle
- middleware functions can perform the following tasks:
    - execute any code
    - make changes to the request and response objects
    - end the req-res cycle
    - call the next middleware function in the stack

## Application-level middleware
- example shows a middleware function with no mount path and is executed every time the app receives a request:
```
var express = require('express')
var app = express()

app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})
```
- example showing a middleware function mounted on the /user/:id path
```
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```
- example of loading a series of middleware functions at mount point with mount path:
```
app.use('/user/:id', function (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}, function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```
- example of a middleware sub-stack that handles GET requests to the /user/:id path:
```
app.get('/user/:id', function (req, res, next) {
  console.log('ID:', req.params.id)
  next()
}, function (req, res, next) {
  res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', function (req, res, next) {
  res.end(req.params.id)
})
```
## Router-level middleware
* Router-level middleware works in the same way as app-level middleware but it is bound to an instance of express.Router().
- example code replicates the middleware system:
```
var express = require('express')
var app = express()
var router = express.Router()

// a middleware function with no mount path. This code is executed for every request to the router
router.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use('/user/:id', function (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}, function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get('/user/:id', function (req, res, next) {
  // if the user ID is 0, skip to the next router
  if (req.params.id === '0') next('route')
  // otherwise pass control to the next middleware function in this stack
  else next()
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', function (req, res, next) {
  console.log(req.params.id)
  res.render('special')
})

// mount the router on the app
app.use('/', router)
To skip the rest of the router’s middleware functions, call next('router') to pass control back out of the router instance.

This example shows a middleware sub-stack that handles GET requests to the /user/:id path.

var express = require('express')
var app = express()
var router = express.Router()

// predicate the router with a check and bail out when needed
router.use(function (req, res, next) {
  if (!req.headers['x-auth']) return next('router')
  next()
})

router.get('/user/:id', function (req, res) {
  res.send('hello, user!')
})

// use the router and 401 anything falling through
app.use('/admin', router, function (req, res) {
  res.sendStatus(401)
})
```
## Error-handling middleware
* example:
```
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```
## Built-in middleware
* Express has the following built in middleware functions:
    - express.static serves static assets such as HTML files, images, and so on.
    - express.json parses incoming requests with JSON payloads. NOTE: Available with Express 4.16.0+
    - express.urlencoded parses incoming requests with URL-encoded payloads. NOTE: Available with Express 4.16.0+

## Third-party middleware
* following example illustrates installing and loading cookie parsing middleware function:
```
var express = require('express')
var app = express()
var cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```
# ExpressJS Middleware
* This is pretty much the same summary of middleware seen above.  Pretty cool flow chart showing whats going on:

![middleware flowchart](/assets/middleware_desc.jpg)

## Third Party Middleware
* following is a list of useful parsers

- body-parser
- used to parse the body of request which have payloads attached to them
```
var bodyParser = require('body-parser');

//To parse URL encoded data
app.use(bodyParser.urlencoded({ extended: false }))

//To parse json data
app.use(bodyParser.json())
```
- cookie-parser
- parses Cookie header and populate req.cookies with an object keyed by cookie names
- include the following in index.js:
```
var cookieParser = require('cookie-parser');
app.use(cookieParser())
```
# Express middleware list

* Great list  of modules here:
<https://expressjs.com/en/resources/middleware.html>