# User Modeling
* web apps need to model sensitive information about users.
* developers have a responsibility to store this information safely.
* passwords should always be encrypted using a hashing algorithm
* models with sensitive data should **NEVER** be sent to client applications

# Cryptography
* Cryptographic Cypher Algorithm takes a piece of data and a key and produces encrypted data.
* Data can later be reversed using the same key
* User tokens can be created associating a random string with a user account

# Basic Authorization
* common method used to send a username and password in an HTTP request
* username and password are joined with ':' then 'base64 coded' and placed after the string 'Basic'
* sever decodes Basic Authorization header to retrieve the username and password
- in browsers we get *atob* and *btoa* to convert to/from "Base64 Encoding":
```
let encoded = window.btoa('someusername:P@55w0rD!')
// c29tZXVzZXJuYW1lOlBANTV3MHJEIQ==

let decoded = window.atob('c29tZXVzZXJuYW1lOlBANTV3MHJEIQ==');
// someusername:P@55w0rD!

request({
  method: 'GET',
  url: 'https://api.example.com/login',
  headers: {
    Authorization: `Basic ${encoded}`,
  },
})
.then(handleLogin)
.catch(handleLoginError)
```

- in node app, we can use a node module to do the same:

```
let base64 = require('base-64');

let string = 'someusername:P@55w0rD!';
let encoded = base64.encode(string); // c29tZXVzZXJuYW1lOlBANTV3MHJEIQ==
let decoded = base64.decode(encoded); // someusername:P@55w0rD!
```

