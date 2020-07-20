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


