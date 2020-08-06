# Callbacks and Promises
* JavaScript is synchronous by default, and is single threaded. This means that code cannot create new threads and run in parallel.
- Asynchronicity in Programming Languages
    - Asynchronous means that things can happen independently of the main program flow.
    - Programs internally use interrupts, a signal that’s emitted to the processor to gain the attention of the system.
    - Normally, programming languages are synchronous, and some provide a way to manage asynchronicity, in the language or through libraries. 
- JavaScript
    - JavaScript is synchronous by default and is single threaded. This means that code cannot create new threads and run in parallel.
- Callbacks
    -  callback is a simple function that is passed as a value to another function, and will only be executed when the event happens
    - Callbacks are used everywhere, not just in DOM events.
- Handling errors in callbacks
    - the first parameter in any callback function is the error object: error-first callbacks
- Problem with callbacks
    - callbacks add a level of nesting.  Lots of callbacks, things get complicated.
- Alternative to callbacks .......
* PROMISES
     - way to deal with asynchronous code in JavaScript, without writing too many callbacks in your code.
     - defined as a proxy for a value that will eventually become available.
- Creating a promise
    - The Promise API exposes a Promise constructor, which you initialize using new Promise():
- Consuming a promise
    - Running checkIfItsDone() will execute the isItDoneYet() promise and will wait for it to resolve, using the then callback, and if there is an error, it will handle it in the catch callback.
- Chaining promises
    -example of chaining promises is given by the Fetch API, a layer on top of the XMLHttpRequest API, which we can use to get a resource and queue a chain of promises to execute when the resource is fetched.
- Handling errors
    - When anything in the chain of promises fails and raises an error or rejects the promise, the control goes to the nearest catch() statement down the chain
- Cascading errors
    - If inside the catch() you raise an error, you can append a second catch() to handle it
- Orchestrating promises
    - If you need to synchronize different promises, Promise.all() helps you define a list of promises, and execute something when they are all resolved.

# MDN on Asynchronous
* General asynchronous programming concepts
    - In this article we'll run through a number of important concepts relating to asynchronous programming, and how this looks in web browsers and JavaScript. You should understand these concepts before working through the other articles in the module.

* Introducing asynchronous JavaScript
    - In this article we briefly recap the problems associated with sychronous JavaScript, and take a first look at some of the different asynchronous JavaScript techniques you'll encounter, showing how they can help us solve such problems.
* Cooperative asynchronous JavaScript: Timeouts and intervals
    - Here we look at the traditional methods JavaScript has available for running code asychronously after a set time period has elapsed, or at a regular interval (e.g. a set number of times per second), talk about what they are useful for, and look at their inherent issues.
* Handling async operations gracefully with Promises
    - Promises are a comparatively new feature of the JavaScript language that allow you to defer further actions until after the previous action has completed, or respond to its failure. This is really useful for setting up a sequence of operations to work correctly. This article shows you how promises work, where you'll see them in use in WebAPIs, and how to write your own.
* Making asynchronous programming easier with async and await
    - Promises can be somewhat complex to set up and understand, and so modern browsers have implemented async functions and the await operator. The former allows standard functions to implicitly behave asynchronously with promises, whereas the latter can be used inside async functions to wait for promises before the function continues. This makes chaining promises simpler and easier to read.
* Choosing the right approach
    - To finish this module off, we'll consider the different coding techniques and features we've discussed throughout, looking at which ones you should use when, with recommendations and reminders of common pitfalls where appropriate.

# Using Promises
* A Promise is an object representing the eventual completion or failure of an asynchronous operation.

* Guarantees
- Unlike passed in callbacks a promise comes with some guarantees:
        - Callbacks will never be called before the completion of the current run of the JavaScript event loop.
        - Callbacks added with then(), as above, will be called even after the success or failure of the asynchronous operation.
        - Multiple callbacks may be added by calling then() several times. Each callback is executed one after another, in the order in which they were inserted
* Chaining
    - Basically, each promise represents the completion of another asynchronous step in the chain.
* Promise rejection events
    - rejectionhandled
         -Sent when a promise is rejected, after that rejection has been handled by the executor's reject function.
    - unhandledrejection
        - Sent when a promise is rejected but there is no rejection handler available.
* Creating a promise around an old callback API
    - A Promise can be created from scratch using its constructor. This should be needed only to wrap old APIs.
    - Basically, the promise constructor takes an executor function that lets us resolve or reject a promise manually.
* Composition
    - Promise.resolve() and Promise.reject() are shortcuts to manually create an already resolved or rejected promise respectively. This can be useful at times.

* Timing
    - To avoid surprises, functions passed to then() will never be called synchronously, even with an already-resolved promise:
* Nesting 
    - Simple promise chains are best kept flat without nesting, as nesting can be a result of careless composition
    - Nesting is a control structure to limit the scope of catch statements.

# Video on promises and fetch
    - a good visual representation of the readings above.  was good to see the fetch and promise demonstrated on video.  helps the understanding of their use.

# Promises in Sixteen Minutes
* It can be tricky to wrap your head around exactly what they are and how to use them when you are thinking about them in the abstract.
 * Land before promises
    - JavaScript is a single-threaded language, which means that it can only do one thing at a time
        - giving an asynchronous function a callback function but the callback is pushed back in the stack
        - negative impact on how well your code works
* Land not before promises
    - A promise represents the eventual result of an asynchronous operation. The primary way of interaction with a promise is through its then method, which registers callbacks to receive either a promise’s eventual value or the reason why the promise cannot be fulfilled.
    - A promise is basically a container for an asynchronous action — what this tells us is that, at a minimum, promises have to give us everything in terms of capability that vanilla async callbacks give us, because a promise is something that is taking a vanilla async callback and putting it into a format that will be less heinous to actually implement.
        1. A promise takes an executor; some kind of function that were using whose return results we need to control asynchronously
        2. A promise has internal state.  can change from pending to fullfilled or rejected.  determines which callback fucntion we run
        3. A promise has value. the value cannot change once we get it
        4. A promise has to have access to a 'then' method.  takes the place of nesting promises

* Making promises
    - javascript has a promise constructor which we pass it our executor and callbacks
    - More frequently we’ll see that promises are supported and baked into other libraries that our application uses.

# JavaScript Promises
* A promise can be:
    - fulfilled - The action relating to the promise succeeded
    - rejected - The action relating to the promise failed
    - pending - Hasn't fulfilled or rejected yet
    - settled - Has fulfilled or rejected

var promise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…

  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});

* XMLHttpRequest
 
 function get(url) {
  // Return a new promise.
  return new Promise(function(resolve, reject) {
    // Do the usual XHR stuff
    var req = new XMLHttpRequest();
    req.open('GET', url);

    req.onload = function() {
      // This is called even on 404 etc
      // so check the status
      if (req.status == 200) {
        // Resolve the promise with the response text
        resolve(req.response);
      }
      else {
        // Otherwise reject with the status text
        // which will hopefully be a meaningful error
        reject(Error(req.statusText));
      }
    };

    // Handle network errors
    req.onerror = function() {
      reject(Error("Network Error"));
    };

    // Make the request
    req.send();
  });
}

* Chaining
    -  chain thens together to transform values or run additional async actions one after another

**There are a ton of examples here that i've already covered in MD**
https://web.dev/promises/


# Using Fetch
* The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. 
    - provides global fetch() method
* Supplying request options
    - The fetch() method can optionally accept a second parameter, an init object that allows you to control a number of different settings

* Sending a request with credentials included
    - To cause browsers to send a request with credentials included, even for a cross-origin call, add credentials: 'include' to the init object you pass to the fetch() method.
* Uploading JSON data
    - Use fetch() to POST JSON-encoded data.
* Uploading a file
    - Files can be uploaded using an HTML <input type="file" /> input element, FormData() and fetch().
* Uploading multiple files
    - Files can be uploaded using an HTML <input type="file" multiple /> input element, FormData() and fetch().
* Processing a text file line by line
    - The chunks that are read from a response are not broken neatly at line boundaries and are Uint8Arrays, not strings.
    - If you want to fetch a text file and process it line by line, it is up to you to handle these complications.
* Checking that the fetch was successful
    - A fetch() promise will reject with a TypeError when a network error is encountered or CORS is misconfigured on the server-side, although this usually means permission issues or similar — a 404 does not constitute a network error, for example.
    - An accurate check for a successful fetch() would include checking that the promise resolved, then checking that the Response.ok property has a value of true. 
* Supplying your own request object
    - Instead of passing a path to the resource you want to request into the fetch() call, you can create a request object using the Request() constructor, and pass that in as a fetch() method argument

* Headers
    - The Headers interface allows you to create your own headers object via the Headers() constructor. A headers object is a simple multi-map of names to values

* Response objects
    -  Response instances are returned when fetch() promises are resolved.
    - Response.status — An integer (default value 200) containing the response status code.
    - Response.statusText — A string (default value "OK"), which corresponds to the HTTP status code message.
    - Response.ok — seen in use above, this is a shorthand for checking that status is in the range 200-299 inclusive. This returns a Boolean.
* Body
- Following types:
    - ArrayBuffer
    - ArrayBufferView (Uint8Array and friends)
    - Blob/File
    - string
    - URLSearchParams
    - FormData

# Fetching Data
* fetch() is not the only way JS can deal with data from servers, but it might be the easiest.

* Big picture

    1. fetch() makes network request to a url and returns a promise.
    2. That promise resolves with a response object when the remote server responds with headers.
    3. To read the response body, we have to call a response method on it, like text() or json(), which will return another promise whose resolve value is the body of the response.

* Breakdown
    - fetch() creates a promise that resolves with a response object.
* Working with example

    fetch(url)
  .then(function(theResponseObject) {
    return theResponseObject.methodToGetToData()
  })
  .then(function(myUsableData) {
    // manipulate/show/log our data 
  })
  .catch(function(error)
   // error handling here
  );
    - fetch() resolves with a response object, which is taken into our first then() method
    - second then(), we actually get to manipulate our data. I’m just using document.write()
    - So for every fetch() whose data you want to show or manipulate you will need at least two then() methods: the first to return the response method that retrieves your data, and the second then to actually work with the data.
* Fetch isn't for getting
    -  fetch() can take a second argument, a request. You simply pass in an object to fetch() that specifies the type of request you want to make, along with the headers and body and whatever else is needed
