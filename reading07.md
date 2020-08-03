 # Domain Modeling 
* Domain modeling is the process of creating a conceptual model in code for a specific problem. An entity that stores data in properties and encapsulates behaviors in methods is commonly referred to as an object-oriented model. A domain model that's articulated well can verify and validate the understanding of a specific problem among various stakeholders.

- When modeling a single entity that'll have many instances, build self-contained objects with the same attributes and behaviors.
- Model its attributes with a constructor function that defines and initializes properties.
- Model its behaviors with small methods that focus on doing one job well.
- Create instances using the **new** keyword followed by a call to a constructor function.
- Store the newly created object in a variable so you can access its properties and methods from outside.
- Use the **this** variable within methods so you can access the object's properties and methods from inside.

# Chapter 6 HTML/CSS Tables

* A table represents information in a grid format.

- <table>
    - creates table
- <tr>
    - table row
- <td>
    - table data
- <th>
    - table heading

* Spanning columns
    - colspan attribute can be used on a <th> or <td> element and indicates how many columns that the cell should run across.

* Spanning rows
    - the rowspan attribute can be used on a <td> or <th> element to indicate how many rows a cell should span down the table.

* Long tables
    - <thead>
        - the headings of the table should sit inside this element
    - <tbody>
        - the body should sit inside this element
    - <tfoot>
        - the footer belongs inside this element

# Chapter 3 JAVASCRIPT Function, Methods, Objects

* Function
    - series of statements put together to perform a task
    - information passed into functions is called **Parameters**
    - functions are expected to return a **value**
    - See pgs 92-95
    - a **function declaration** creates a function you can call
    - a function treated as an expressing is called a **function expression**
    - a function with no name is called an **anonymous function**
    - Immediatley Invoked Function Expression 'IIFE' 'iffy'
        - executed once as interpreter comes across them.
        - used: 1. As an argument when a fucntion is called 'to calculate a value for that function'
                2. To assign the value of a property to an object
                3. In event handlers and listeners to perform a task when an event occurs.
                4. To prevent conflicts between two scripts that might use the same variable names.
* Variable scope
    - local variable = variable declared inside a function
    - global variable = variable declared outside a fuction
        - require more memory
* Objects 
    - a group of variables and functions to create a model of something you would recognize from the real world
    - variables become known as properties
    - functions become known as methods
    - key/value pairs
        - object cannot have 2 keys with the same name
    - property names and values can be updated in an object 
        - hotel.name = 'park' - changes value of name to 'park'
        - hotel['name'] = 'park' - updates the property from name to 'park'
    - arrays are objects
        
* Built in objects
    - browsers come withe a set of built in objects that represent things like the browser window and the current web page shown in that window

    - window object
        - represents the current browser window or tab.
        - topmost object in the Browser Object Model
        - see pg 124 
    - document object
        - represents the web page loaded into the current browser window or tab.
        - see pg 126
    - string object
        - whenever you have a value that is a string you an use the properties and methods of the string object on that value
    - number object
        - whenever you have a value that is a number you can use the methods and properties of the number object on it
    - math object
        - the math object has properties and methods for mathematical constants and functions
    - date and time object
        - see pg 137
        