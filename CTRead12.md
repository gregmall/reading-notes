# Why you should use BCrypt to has passwords
## Hashed password solutions fall short
- examples:
- **Plain text passwords**
  - makes use of only letters
  - often used over several different logins
  - easily hacked
- **One way hash**
  - server does not store plain text passwords to authenticate user
  - hashing algorithm applied to make more secure
  - hackers can still guess passwords until they gain access
- **'Salting' the password**
  - adds a long string of bytes to the password
  - if hacker has access to source code, they will be able to find the salt string
- **Random 'salt' for each user
  - bette than just salting but hacker can still guess.  Just takes more time

## The BCrypt Solution
* based on Blowfish block cipher cryptomatic algorithm and takes the form of an adaptive hash function
* Key Factor
  - sounds fancy? i guess it influences hash output 
  - lots of fancy explanation of this solution.  Sounds like an infomercial.  I guess is somehow slows down the cracking process
  - neat

# Understanding bcrypt

* **What is bcrypt**
- b is for Blowfish and crypt is the name of the hashing function used by the UNIX password system
- combines they expensive key setup phase of blowfish with a variable number of iterations to increase the workload and duration of hash calculations.  
- requires a salt by default
- uses a 128-bit salt and encrypts a 192-bit magic value 
* **How does bcrypt work**
- phase 1
  - function called EksblowFishSetup is used to initialize state of ekblowfish
  - crypt runs key schedule  performing key derivation to derive a set of subkeys from a primay key
- phase 2
  - magic value is encrypted 64 times useing eksblowfish in ECB mode with the state from previous phase
![bcrypt example](/assets/bcrypt-algo.png)
- achieves the three core properties of a secure password function:
  - It's preimage resistant.
  - The salt space is large enough to mitigate precomputation attacks, such as rainbow tables.
  - It has an adaptable cost.
* **Best Practices**
- cost to set for function
  - work factor
- OWASP recommends as a common rule of thumb for work factor setting
  - Perform UX research to find what are acceptable user wait times for registration and authentication.
  - If the accepted wait time is 1 second, tune the cost of bcrypt for it to run in 1 second on your hardware.
  - Analyze with your security team if the computation time is enough to mitigate and slow down attacks.

* **Implementing bcrypt**

```
npm install bcrypt
```
```
// app.js

const bcrypt = require("bcrypt");
const saltRounds = 10;
const plainTextPassword1 = "DFGh5546*%^__90";
```

* Technique 1: Generate a salt and hash on separate function calls
```
// app.js

const bcrypt = require("bcrypt");
const saltRounds = 10;
const plainTextPassword1 = "DFGh5546*%^__90";

bcrypt
  .genSalt(saltRounds)
  .then(salt => {
    console.log(`Salt: ${salt}`);

    return bcrypt.hash(plainTextPassword1, salt);
  })
  .then(hash => {
    console.log(`Hash: ${hash}`);

    // Store hash in your password DB.
  })
  .catch(err => console.error(err.message));
```
* Technique 2: Auto-generate a salt and a hash
```
// app.js

const bcrypt = require("bcrypt");
const saltRounds = 10;
const plainTextPassword1 = "DFGh5546*%^__90";

bcrypt
  .hash(plainTextPassword1, saltRounds)
  .then(hash => {
    console.log(`Hash: ${hash}`);

    // Store hash in your password DB.
  })
  .catch(err => console.error(err.message));
```

## Simplifying Password Management with Auth0
* Can minimize the overhead of hashing salting and password management with Auth0
* Auth0 helps prevent critical identity data from falling into the wrong hands
  - they really want you to sign up for an Auth0 account.  Im sure they'll ask for a credit card number