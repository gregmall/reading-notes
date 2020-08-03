# Template literals
    - Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them.
    - Syntax: `string text ${expression} string text`
    - Template literals are enclosed by the backtick
    - can contain placeholders
* multi-line strings
    - Any newline characters inserted in the source are part of the template literal.
    - Syntax: console.log(`string text line 1
      string text line 2`);
* expression interpolation
    - Syntax:
     let a = 5;
     let b = 10;
     console.log(`Fifteen is ${a + b} and
     not ${2 * a + b}.`);

# Google Developer
- Strings in JavaScript have been historically limited
- **Template Strings** fundamentally change that.
    - string interpolation
    - embedded expressions
    - multiline strings without hacks
    - string formatting
    - string tagging for safe HTML escaping, localization and more.
- Template strings use back-ticks
- whitespace inside the backticks are considered part of the string 

* Template Strings are in Chrome 41 beta+, IE Tech Preview, Firefox 35+ and io.js. Practically speaking if you would like to use them in production today, they're supported in major ES6 Transpilers, including Traceur and 6to5. Check out our Template Strings sample over on the Chrome samples repo if you'd like to try them out. You may also be interested in ES6 Equivalents in ES5, which demonstrates how to achieve some of the sugaring Template Strings bring using ES5 today.
* Template Strings bring many important capabilities to JavaScript. These include better ways to do string & expression interpolation, multiline strings and the ability to create your own DSLs.
* One of the most significant features they bring are tagged templates - a critical feature for authoring such DSLs. They receive the parts of a Template String as arguments and you can then decide how to use the strings and substitutions to determine the final output of your string.

# CSS Tricks
* The Template Literal is a new way to create a string.
    - use back ticks instead of quotes.

* Multi-line
    - example: 
        var myMultiString= `This will be
        on two lines!`;
    - This will produce a string with a new line in it.
* Expressions
    - In the new Template Literal syntax we have what are called expressions
    - example:
        let name = `Ryan`;

        console.log(`Hi my name is ${name}`);
    - The ${} syntax allows us to put an expression in it and it will produce the value

* HTML Templates
    - With the ability to have multi-line strings and use Template Expressions to add content into our string, this makes it really nice to use for HTML templates in our code.

# MDN forEach

* The forEach() method executes a provided function once for each array element.
- syntax: arr.forEach(callback(currentValue [, index [, array]])[, thisArg])

* Description 
    - forEach() calls a provided callback function once for each element in an array in ascending order. It is not invoked for index properties that have been deleted or are uninitialized.

# For Loops VS forEach in Javascript

##THERE CAN BE ONLY ONE
    - but seriously...

    - forEach only work on arrays
    - if you want to count, use a for loop
    - forEach is kinda easier to understand and it is idiomatic.  They read better.  
