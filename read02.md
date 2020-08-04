# Applying Atomic Design
**PART ONE**
* NEED TO KNOW:
    - Familiarity with Atomic Design Terms
        - found here: https://atomicdesign.bradfrost.com/chapter-2/
- Start Big and work your way down
    - organisms are large sections that we can easily extract from the page
    - further divide each organism into molecules which are sections that we can easily extract from an organism
    - organisms can contain other organisms 
    - further extract atoms from molecules
    - atoms cannot be broken down further

**PART TWO**

* NEED TO KNOW
    - familiarity with atomic design terms (see above link)
    - ability to read ReactJs code
    - Familiarity with ES6

- a folder structure should follow a consistent pattern to allow you to browse through the files quickly
* Start small and work your way up
    - when building, its the exact opposite as when break down components

**MORE EXAMPLES**

* atomic design: atoms to molecules to organisms to templates to pages
    - Interfaces are made up of smaller components. This means we can break entire interfaces down into fundamental building blocks and work up from there. That’s the basic gist of atomic design.

Lack of governance can lead to: 
    - the developer is wasting time by re-implementing patterns you already have
    - the developer is contributing to the inflation of your stylesheets by adding the same styles again and again out of lack of awareness that they already exist
    - the developer will notice that his styles interfere with other styles and will add a surplus of css overrides to force his component into shape
    - the developer will not notice that his styles interfere with other styles and will break the barstool in the other bar
- component driven front end development promises simplification

# Thinking in React

* Start with a mock
    - step 1: Break the UI into a component hierarchy
        - draw boxes around every component
        - use the same techniques for deciding if you should create a new function or object to determine what to box
        - UI and data models tend to adhere to the same information architecture
    - step 2: Build a static version in React
        - build a version that takes your data model and renders the UI but has no interactivity
        - build components that reuse other components and pass data using props which pass data from parent to child
        - can build top down or bottom up
        - at the end of this step you'll have a library of reusable components that render your data model
    - step 3: Identify the minimal representation of UI state
        - you need to be able to trigger changes to your underlying data model.  React achieves this with state.
        - think of the minimal set of mutable state that your app needs
        - don't repeat yourself
    - step 4: Identify where your state should live
        - we need to identify which component mutates, or owns, this state
        - for each piece of state in your application:
            - Identify every component that renders something based on that state.
            - Find a common owner component (a single component above all the components that need the state in the hierarchy).
            - Either the common owner or another component higher up in the hierarchy should own the state.
            - If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common owner component.
    - step 5: Add inverse data flow
        - React makes data flow explicit to help you understand how your program works but it does require more typing than traditional two-way data binding

    # UI Components by Design
    * Express design as working components
        - Components let you split the UI into independent, reusable pieces, and think about each piece in isolation.
        - Designers can draw a parallel between frameworks like Atomic Design and the popular concepts coming out of the React community.
    * Convergence of language
        - Though both the designer and developer are thinking in a way that makes sense to themselves, they’re speaking different languages. As a result, the conversation’s fraught with misinterpretations and mistakes.
    * Two types of components:
        1. Foundation Components are the primary expression of the design language of the system. They’re the defining parts of the experience, and very targeted in scope. They ensure a consistent underlying interface. UI Developers on the design team will build them.
        2. Application Components are specific to one of the applications being built, and not seen as a defining, foundational part of the UI. They’re usually larger in scope, and almost always composed of one or many Foundation Components. Some Application Components may eventually transition into Foundation Components. The application teams will build them.
    * Component-centric workflow
        - circular flow marked by tight feedback loops between designers, UI developers, and application developers
    * Design
        - A designer starts by designing a part of the experience, keeping in mind the overall context of the application and the current components available in the design language.
        - As an application design materializes, break it down into its composite parts, its components.
    * Isolate and elaborate
        - The designer collaborates with a UI developer to isolate core UI elements so that they can elaborate on their structure, appearance, and behaviors
        -  In a component architecture, components are independent and reusable across various contexts.
    * Build
        - Using the agreed specification, the UI developers build the Foundation Component as a React component
        - decouple the Foundation Component from the application.
    * Integrate and learn
        - Foundation Components are published so that application developers can bring them into applications and assemble them into larger, more complex components
        - Abstracting the component behind a small, but flexible, interface makes it easy for both designers and developers to discuss it.

# What Are JavaScript Callbacks?
 * a callback is a function that is to be executed after another function has finished executing.
- needed because javascript is an even driven language.  Keeps executing while listening for other events
- callbacks are a way to make sure certain code doesn't execute until other code has already finished execution.

# JavaScript Callback Functions

- A function is a block of code that will be executed when you call it
- A function is written as a code block inside curly { } braces, preceded by the function keyword
- The code inside the function will be executed when you call the function
- common name for a function passed in to another function is called a callback function
- In computer programming, a callback is a piece of executable code that is passed as an argument to other code, which is expected to call back (execute) the argument at some convenient time.
- The invocation may be immediate as in a synchronous callback or it might happen at later time, as in an asynchronous callback.

# First Class Functions

* A programming language is said to have First-class functions when functions in that language are treated like any other variable. For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.


# Callback Function

* A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action
- callbacks are often used to continue code execution after an asynchronous operation has completed 

# JavaScript Classes

* Class Syntax
    - basic syntax: 
    class MyClass {
        // class methods
         constructor() { ... }
        method1() { ... }
        method2() { ... }
        method3() { ... }
        ...
    }
    - Then use new MyClass() to create a new object with all the listed methods.

    - The constructor() method is called automatically by new, so we can initialize the object there.

    Example: 
    class User {

        constructor(name) {
          this.name = name;
       }

        sayHi() {
          alert(this.name);
       }

    }

       // Usage:
      let user = new User("John");
       user.sayHi()

* What is a class?
    - In JavaScript, a class is a kind of function.
    // rewriting class User in pure functions

    // 1. Create constructor function
    function User(name) {
        this.name = name;
    }
// a function prototype has "constructor" property by default,
// so we don't need to create it

// 2. Add the method to prototype
        User.prototype.sayHi = function() {
        alert(this.name);
    };

// Usage:
    let user = new User("John");
    user.sayHi();

* Class Expression
    - Just like functions, classes can be defined inside another expression, passed around, returned, assigned, etc.
    - If a class expression has a name, it’s visible inside the class only
* Getters/setters
    - Just like literal objects, classes may include getters/setters, computed properties etc.
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

# Intro to Object Oriented Programming
* Objects in JavaScript
    - an object can be enhanced and that makes it possible to create an instance of an implicit class without the need to actually create the class
* Classes in JavaScript
    - An object is an instance of a class
    - using a class you can create objects and they all share methods and properties

    - A good object oriented way of defining classes should provide:
        - a simple syntax to declare a class
        - a simple way to access to the current instance AKA 'this'
        - a simple syntax to extend a class
        - a simple way to access the super class instance AKA 'super'
        - a simple way of telling if an object is an instance of a particular class.

* Classes in JavaScript 5
    - JavaScript classes, introduced in ECMAScript 2015, are primarily syntactical sugar over JavaScript’s existing prototype-based inheritance
    - key concept: prototype-based inheritance

* New operator in JavaScript
    - The **new** operator lets developers create an instance of a user-defined object type or of one of the built-in object types that has a constructor function.
* Functional programming
    - In JavaScript functions are first class citizens (e.g. you can pass a function to another function) and it provides features like bind , call or apply which are base constructs used in functional programming.

# Object Methods

* "this"
    - It’s common that an object method needs to access the information stored in the object to do its job.
    - To access the object, a method can use the this keyword.
* "this" is not bound
    - In JavaScript, keyword this behaves unlike most other programming languages. It can be used in any function
* Arrow functions have no "this"
    - Arrow functions are special: they don’t have their “own” this. If we reference this from such a function, it’s taken from the outer “normal” function.

- Functions that are stored in object properties are called “methods”.
- Methods allow objects to “act” like object.doSomething().
- Methods can reference the object as this.
- The value of this is defined at run-time.

- When a function is declared, it may use this, but that this has no value until the function is called.
- A function can be copied between objects.
- When a function is called in the “method” syntax: object.method(), the value of this during the call is object.
- Please note that arrow functions are special: they have no this. When this is accessed inside an arrow function, it is taken from outside.