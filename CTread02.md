# Clean Code
* was unable to find more from this book.  Would like to see it if someone can provide a link.  Was an interesting and informative first chapter

# Array Methods
* 10 JavaScript array methods you should know
1. forEach()
    -  loops over array's items
2. includes()
    -  checks if the array contains the item passed in the method.
    - returns true or false
3. filter()
    -  creates a new array with only elements that pass the condition in the provided function.
    example:   
    ```
    const arr = [1, 2, 3, 4, 5, 6];

  // item(s) greater than 3
  const filtered = arr.filter(num => num > 3);
  console.log(filtered); // output: [4, 5, 6]

  console.log(arr); // output: [1, 2, 3, 4, 5, 6]
  ```
4. map()
    - creates new array by calling the provided function in every element
5. reduce()
    - applies a function against an accumulator and each element in the array to reduce it to a single value
    example:
    ```
      const arr = [1, 2, 3, 4, 5, 6];

  const sum = arr.reduce((total, value) => total + value, 0);
  console.log(sum); // 21
  ```
6. some()
    - checks if at least one of the array's items passed the condition.
    - returns true or false
7. every()
    - checks if all the array's items passed the condition.
    - returns true or false
8. sort()
    - used to arrange/sort array's items in either ascending or descending order
9. Array.from()
    - Changes all things that are array like or iterable into a true array.
    - especially when working with DOM
    - result allows for use of other methods (reduce,map,filter,etc)
    example:
```
  const name = 'frugence';
  const nameArray = Array.from(name);

  console.log(name); // output: frugence
  console.log(nameArray); // output: ['f', 'r', 'u', 'g', 'e', 'n',

    // I assume that you have created unorder list of items in our html file.

  const lis = document.querySelectorAll('li');
  const lisArray = Array.from(document.querySelectorAll('li'));

  // is true array?
  console.log(Array.isArray(lis)); // output: false
  console.log(Array.isArray(lisArray));  // output: true
```
10. Array.of()
    - creates an array from every argument passed into it.
    example:
  const nums = Array.of(1, 2, 3, 4, 5, 6);
  console.log(nums); // output: [1, 2, 3, 4, 5, 6]

# Array Method Cheat sheet
 * Super nice cheat sheet of array methods.  I have printed it and will use it for reference. 

# Class Syntax

* Basic syntax:
```
class MyClass {
  // class methods
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```
- use new MyClass() to creat new object with all the listed methods
- constructor() method is called automoatically by 'new'
example:
```
 class MyClass {
  // class methods
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```

* What is a class?
- a class is a kind of function
class User {
  constructor(name) { this.name = name; }
  sayHi() { alert(this.name); }
}

// class is a function
```
alert(typeof User); // function

// ...or, more precisely, the constructor method
alert(User === User.prototype.constructor); // true

// The methods are in User.prototype, e.g:
alert(User.prototype.sayHi); // alert(this.name);

// there are exactly two methods in the prototype
alert(Object.getOwnPropertyNames(User.prototype)); // constructor, sayHi
```
* Class expression
- classes can be defined inside another expression, passed around, assigned, etc.
example:
```
let User = class {
  sayHi() {
    alert("Hello");
  }
};
```

* Getters/setters
- classes may include getters/setters, computed properties
example:
```
class User {

  constructor(name) {
    // invokes the setter
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    if (value.length < 4) {
      alert("Name is too short.");
      return;
    }
    this._name = value;
  }

}

let user = new User("John");
alert(user.name); // John

user = new User(""); // Name is too short.
```
* Computed names [...]
- computed method name using brackets
example:
```
class User {

  ['say' + 'Hi']() {
    alert("Hello");
  }

}

new User().sayHi()
```
* Class fields
- syntax that allows to add any properties
example:
```
class User {
  name = "John";

  sayHi() {
    alert(`Hello, ${this.name}!`);
  }
}

new User().sayHi(); // Hello, John!
```
* Summary
- basic class syntax looks like this:
```
 class MyClass {
  prop = value; // property

  constructor(...) { // constructor
    // ...
  }

  method(...) {} // method

  get something(...) {} // getter method
  set something(...) {} // setter method

  [Symbol.iterator]() {} // method with computed name (symbol here)
  // ...
}
```
# Classes MDN
* Classes are a template for creating objects
- encapsulate data with code to work on that data
* Defining classes
- classes are special functions
- class syntax has 2 components:
    1. class expression
        - can be named or unnamed.
        - name given to a named class expression is local to the class's body.
        
    2. class declaration
        - use the 'class' keyword with the name of class

* Class body and method definitions
- Strict mode
    - code written here is subject to stricter syntax for increased performance
- Constructor
    - special method for creating and initializing an object created with a class. 
    - can only be one constructor in a class
    - can use the 'super' keyword to call the constructor of the super class
- Prototype methods
    - method definitions
- Static methods
    - called without instantiating their class and cannot be called through a class instance

* Sub classing with extends
- used in class declarations to create a class as a child of another class
* Species
- lets you override default constructors
example:
```
class MyArray extends Array {
  // Overwrite species to the parent Array constructor
  static get [Symbol.species]() { return Array; }
}

let a = new MyArray(1,2,3);
let mapped = a.map(x => x * x);

console.log(mapped instanceof MyArray); // false
console.log(mapped instanceof Array);   // true
```
* Super class calls with super
- used to call corresponding methods of super class

# MVC Architecture in 5 minutes
 
 * Separates concerns into 3 buckets:
 1. Model: stores and manages data
    - database as an example 
 2. View: Graphical User Interface
    - visual representation of the data-like chart, diagram, table, form.
    - contains functionality such as buttons and input fields
 3. Controller: Brains of the application
    - connects the model and view

* Benefits of MVC
    - Traditionally used for GUIs
    - Popular in web apps
    - MVC responsibilities are divided between the client and server, compatible with web app architecture
    - MVC is helpful design pattern when planning development
    - Separation of Concerns: that code is divided based on function to either the model, view, or controller bucket
    - Works well with Ruby on Rails
    - Loosely Coupled
    - Removes unnecessary dependencies
    - Reuseable without modification
    - MVC makes model classes reusable without modification
    - Code reuse
    - Extendable code
    - High Cohesion
    - Easier to maintain or modify
    - Supports Multiple views
    - Each part can be tested independently (Model, view, controller)

# MVC Video
* this is a great video further explaining MVC.
