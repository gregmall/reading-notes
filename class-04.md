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
    - 

