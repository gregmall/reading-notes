# Promise
- proxy value not necessarily known when promise is created
- one of 3 states:
    - pending: neither fulfilled nor rejected
    - fulfilled: operation completed successfully
    - rejected: operation failed
* Chained promise
- The methods promise.then(), promise.catch(), and promise.finally() are used to associate further action with a promise that becomes settled. These methods also return a newly generated promise object, which can optionally be used for chaining
* Constuctor
- Promise()
Creates a new Promise object. The constructor is primarily used to wrap functions that do not already support promises.
* Static method
- Promise.all(iterable)
    - Wait for all promises to be resolved, or for any to be rejected.
    - If the returned promise resolves, it is resolved with an aggregating array of the values from the resolved promises ,in the same order as defined in the iterable of multiple promises.
    - If it rejects, it is rejected with the reason from the first promise in the iterable that was rejected.
- Promise.allSettled(iterable)
    - Wait until all promises have settled (each may resolve or reject).
    - Returns a promise that resolves after all of the given promises have either resolved or rejected, with an array of objects that each describe the outcome of each promise.
- Promise.race(iterable)
    - Wait until any of the promises is resolved or rejected.
    - If the returned promise resolves, it is resolved with the value of the first promise in the iterable that resolved.
    - If it rejects, it is rejected with the reason from the first promise that was rejected.
- Promise.any(iterable)
    - Takes an iterable of Promise objects and, as soon as one of the promises in the iterable fulfils, returns a single promise that resolves with the value from that promise.
- Promise.reject(reason)
    - Returns a new Promise object that is rejected with the given reason.
- Promise.resolve(value)
    - Returns a new Promise object that is resolved with the given value. If the value is a thenable (i.e. has a then method), the returned promise will "follow" that thenable, adopting its eventual state; otherwise the returned promise will be fulfilled with the value.
    - Generally, if you don't know if a value is a promise or not, Promise.resolve(value) it instead and work with the return value as a promise.
* Instance methods
- Promise.prototype.catch()
    - Appends a rejection handler callback to the promise, and returns a new promise resolving to the return value of the callback if it is called, or to its original fulfillment value if the promise is instead fulfilled.
- Promise.prototype.then()
    - Appends fulfillment and rejection handlers to the promise, and returns a new promise resolving to the return value of the called handler, or to its original settled value if the promise was not handled 
- Promise.prototype.finally()
    - Appends a handler to the promise, and returns a new promise that is resolved when the original promise is resolved. The handler is called when the promise is settled, whether fulfilled or rejected.

# Destructuring
* JavaScript expression that jakes it possible to unpack values from arrays, or properties from objects into distinct variables
- see following link for examples : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

# Spread syntax (...)
* Spread syntax (...) allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.
- see link for examples: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax

# Rest parameters
* The rest parameter syntax allows us to represent an indefinite number of arguments as an array.
- A function's last parameter can be prefixed with ... which will cause all remaining (user supplied) arguments to be placed within a "standard" JavaScript array.
- Only the last parameter can be a "rest parameter"

* Difference between rest parameters and the arguments object
    - rest parameters are only the ones that haven't been given a separate name (i.e. formally defined in function expression), while the arguments object contains all arguments passed to the function;
    - the arguments object is not a real array, while rest parameters are Array instances, meaning methods like sort, map, forEach or pop can be applied on it directly;
    - the arguments object has additional functionality specific to itself (like the callee property).

