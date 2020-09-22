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