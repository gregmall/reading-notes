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