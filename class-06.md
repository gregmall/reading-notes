# Chapter 3 JAVASCRIPT Object literals

* Objects 
    - a group of variables and functions to create a model of something you would recognize from the real world
    - variables become known as properties
    - functions become known as methods
    - key/value pairs
        - object cannot have 2 keys with the same name
    - property names and values can be updated in an object 
        - hotel.name = 'park' - changes value of name to 'park'
        - hotel['name'] = 'park' - updates the property from name to 'park'

# Chapter 5 JAVASCRIPT document object model (DOM)

* DOM 
    - Application Programming Interface API
        - lets programs talk to eachother
* DOM tree
    - model of a web page
    - consistst of four main types of nodes
        1. Document node
            -every element, attribute, and piece of text in html represents its own DOM node
        2. Element node
            - describe the structure of an HTML page (<h1>,<p>, <div> etc)
        3. Attribute node
            - opening tags of html elements carry attributes, these are represented by this node in DOM
        4. Text node
            - once you have accessed an element node, you can reach the text within that element.  This is stored in its own text node
            - cannot have children

* Working with DOM tree
    1. Access the elements
        - select an indvidual element node
            - getElementById()
            - QuerySelector()
        - select multiple elements
            - get ElementByClassname()
            - getElementsByTagName()
            - querySelectorAll()
        - traversing between element nodes
            - parentNode
            - previousSibling/nextSibling
            - firstChild/lastChild
    2. Work with those elements
        - access/update text nodes
            - firstChild property to get the text node
        - work with html content
            - innerHTML
            - textContent
            - createElement()
            - createTextNode()
            - appendChild()/removeChild()
        - access or update attribute values
            - className/id
            - hasAttribute()
            - getAttribute()
            - setAttribute()
            - removeAttribute()
        
    * Accessing elements
        - DOM inquiries may return one element or a NodeList (collection of nodes)
        - methods that return a single element node:
            - getElementById('id')
            - querySelector('css selector')
                - document.querySelector('li.hot')
        - methods that return one or more elements (as an NodeList)
            - getElementsByClassName('class')
            - getElementsByTagName('tagName')
            - querySelectorAll('css selector')

    * Looping through a nodelist
        - (let i=0;i < hotItems.length; i++)
            hotItems[i].className = 'whaterver' 
            see pg 205-208
    * Accessing text only
        - textContent
        - innerText (AVOID)
    * Adding/removing HTML content
        - innerHTML property
            - Approach: can be used on any element
            - Adding content    
                - store new content as string or variable
                - select the element whose content you want to replace
                - set the elements innerHTML property to new string
            - Removing content
                - set innerHTML to an empty string. To remove one element from a DOM fragment (one <li> from a <ul>) need to provide the entire fragment minus that element.
        - DOM manipulation methods
            - Approach: refers to a set of DOM methods that allow you to create element and txt nodes and attach or remove from DOM tree
            - Adding content
                - use DOM method to create new content one node at a time and store it in a variable.  Another DOM method is used to attach it to the right place in the DOM tree.
            - Removing content
                - can be removed from DOM tree using a single method
                


