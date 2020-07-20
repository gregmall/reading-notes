# Chapter 10 JAVASCRIPT Error handling and debugging

* Order of execution
    - order in which statements are executed.
* Execution contexts
    - one global execution context plus each function creates a new execution context
    - Global contex
        - code that is in the script but not a function
    - Function context
        - code that is being run within a function.
* Variable scope
    - Global scope
         - declared outside a function
    - Function level scope
        - variable declared within the function and can only be used within the function

* Exectution context and Hoisting
    - Two phases
        - Prepare
        - Execute
    - Hoisting
        - callfunctions before they have been declared
        - assign a value to a variable that has not yet been declared

* Understanding Errors
    - throws and exception
        - interpreter stops and looks for ;exception-handling code

* Error Objects
    - Can help you find where mistakes are
    - Property description
        - name :  Type of exectuion
        - message: description
        - fileNumber: name of the javascript file
        - lineNumber: line number of error
    
        - Object   :  Description
        - Error: generic error
        - SyntaxError: syntax not followed
        - ReferenceError: tried to reference a viariable not declared
        - TypeError: an unexpected datatype
        - RangeError: numbers not in acceptable range
        
* How to deal with errors
    - Debug the script to fix errors
    - handle errors gracefully

* Debugging workflow
    - where is the problem?
    - What exactly is the problem?

    **USE CONSOLE.LOG()**

    **USE BREAKPOINTS**

    * try
        - specify the code that you think might throw an exception within the try block
    * catch
        - if try block throws an exception cath steps in with an alternative set of code
    * finally
        - the contents of the finally code block with run either way

* Debugging tips
    - Another browser
    - add numbers
    - strip it back
    - explaining the code
    - search
        - Stack Overflow
    - code playgrounds
    - validation tools

* Common errors
 - see pg 485
