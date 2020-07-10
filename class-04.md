# Chapter 4 HTML/CSS Links

* Links allow you to move from one page to another, enabling browsing
* Linking to other sites
    -  Anything clicked between <a> and </a>  will be taken to place specified in href
    -  **absolute** URL
    - **relative** URL are contained within the same site
        - same folder: just file name needed
        - child folder: childfolder/filename
        - grandchild folder: childfolder/grandchildfolder/filename
        - parent folder: ../filename
        - grandparent folder: ../../filename

* Directory Structure
    - top level = root
    - homepage is called index

* Email links
    - mailto: email address
* Opening links in new window
    - a href link **target="blank"**
* Linking to part of same page
    - '#' id attribute
* Linking to specific part of another page 
    - absolute or relative URL followed by '#' followed by id attribute


# Chapter 15 HTML/CSS Layout

* Normal flow
    - Each block level element site on top of the next one
    - CSS property not needed to indicate normal flow

* Relative positioning
    - position: relative
    - moves element in relation to where it would have been in normal flow
    - value of relative
    - up/down: top, bottom.  Horizontal: left, right

* Absolute positioning
    - position: absolute
    - taken out of normal flow and no longer affects the position of other elements on the page
* Fixed positioning
    - position: fixed
    - positions the element in relation to the browser window.  Stays in place when scrolling
    - box offset property is used to control where fixed position appears

* Overlapping elements
    - z-index sometimes referred to as **stacking context**
    - controls which elements sit on top when overlapping
    - the higher the number, the closer the element is to the front

* Floating elements
    - float: right/left
    - take an element in normal flow and place it as far to the left/right of the containing element as possible
    - anything else in the element will flow around the floated element
    - should also specify width to indicate how wide floated element will be
    - can create multi column layouts with float using, width, float and margin

* Fixed width layout
    - usually specified in pixels
    - will stay the same no matter the size of the browser

* Liquid layout
    - uses percentages so the width will stretch to fit the size of the screen

* Layout grid
    -960 pixel wide 12 column grid

* Multiple style sheets
    - modular approach: create separate stylesheets to control typography, layout, forms, tables, etc.
    - use '@import' rule to import each stylesheet


# Chapter 3 JAVASCRIPT Function, Methods, Objects

* Function
    - series of statments put together to perform a task
    - information passed into fucntions is called **Parameters**
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