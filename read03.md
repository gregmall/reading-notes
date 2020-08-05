# Responsive Web Design
- Responsive web design is the practice of building a website suitable to work on every device and every screen size, no matter how large or small, mobile or desktop.

* Responsive vs Adaptive vs. Mobile
- Responsive generally means to react quickly and positively to any change, while adaptive means to be easily modified for a new purpose or situation, such as change.
- Mobile generally means to build a separate website commonly on a new domain solely for mobile users.

* Flexible Layouts
- flexible layout
- media queries
- flexible media

* Flexible Grid
    - Using the flexible grid formula we can take all of the fixed units of length and turn them into relative units

* Media Queries
    - Media queries were built as an extension to media types commonly found when targeting and including styles. Media queries provide the ability to specify different styles for individual browser and device circumstances, the width of the viewport or device orientation for example.
    - There are a couple different ways to use media queries, using the media rule inside of an existing style sheet, importing a new style sheet using the import rule, or by linking to a separate style sheet from within the HTML document. 
* Mobile First
    - The mobile first approach includes using styles targeted at smaller viewports as the default styles for a website, then use media queries to add styles as the viewport grows.
* Viewport
    - Mobile devices generally do a pretty decent job of displaying websites these days. Sometimes they could use a little assistance though, particularly around identifying the viewport size, scale, and resolution of a website. To remedy this, Apple invented the viewport meta tag.

* Flexible Media
    - As viewports begin to change size media doesn’t always follow suit. Images, videos, and other media types need to be scalable, changing their size as the size of the viewport changes.

# All About Floats
* Float is a CSS property
    - used to create entire web layouts.

* What are floats used for?
    - Floats are also helpful for layout in smaller instances.
* Clearing the float
    - Float’s sister property is clear.
    - An element that has the clear property set on it will not move up adjacent to the float like the float desires, but will move itself down past the float.
    - Four values
        - both
        - left
        - right
        - none
* The Great Collapse
    - if the parent element contains nothing but floated elements the hight will collapse
    - An element that has the clear property set on it will not move up adjacent to the float like the float desires, but will move itself down past the float.
    - fixed by clearing float after the floated elements but before the close of the container.
* Techniques for clearing floats
    - The empty div method
        - literally, an empty div.
    - The overflow method
        - set the overflow css property on the parent element
    - The easy clearing method
        - apply a class like "clearfix" 
* Problems with floats
    - Pushdown 
        - symptom of an element inside a floated item being wider than the float itself (typically an image).
    - Double margin bug
        - set display: inline on the float and it will remain block level
    -3px jog
        - set width or height on the affected text
    - Bottom margin bug
        - parent has floated children inside it, bottom margin on those children is ignored by the parent
* Alternatives
    - If you need text wrapping around images, there really aren’t any alternatives for float

# Don't Overthink Grids
 - Context
    - A block level element is as wide as the parent it’s inside
 - Columns
    - <div class="grid">
     <div class="col-2-3">
     Main Content
     </div>
     <div class="col-1-3">
     Sidebar
    </div>
    </div>

  - then
  .col-2-3 {
       width: 66.66%;
    }
   .col-1-3 {
       width: 33.33%;
    }

* Clearing context
    - The parent element will collapse to zero height since it has only floated children. Let’s fix that by clearing it
* Gutters
    - gutters are weird.  use box sizing and apply fixed padding
* Outside Gutters
    - padding on parent
    - restore right padding to last column
* Sass
    - its sassy. succinct with scss/compass
* Modules
    - are pretty cool

# CSS Floats Explained by Riding an Escalator

- Respect the pass lane
    - this is a pretty hilarious metaphor for floats
    - escalator makes total sense
- Floats: left and right
    - again ,the escalator analogy is perfect for this
- The Clear Property
    - Clear” allows elements to specify where they should align in comparison to the floated elements.
