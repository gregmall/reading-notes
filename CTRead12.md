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
![bcrypt example]</assets/bcrypt-algo.png>

