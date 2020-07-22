# Chart.js Article

- Chart.js is an amazing resource for creating charts and graphs for a project.  This article gives instructions on how to create bar graphs and pie charts and also provides the script necessary to implement them in your work.  I have book marked the site and know I will be using it often going forward.

# Basic usage of canvas

- Canvas element
    - can be styled with margin, border, background etc.
    - easy to define fallback
- Rendering context
    - creates a fixed size drawing surface that exposes one or more rendering contexts, which are used to create and manipulate the content shown
    - method is called getContext()
        - takes one parameter, the type of context
    
- Checking for support
    - test for the presents of getContext() method

# Drawing with canvas

-  The grid
    - coordinate space
    - Normally 1 unit in the grid corresponds to 1 pixel on the canvas.

- Drawing rectangles
    - only supports two primitive shapes: rectangles and paths
    - All other shapes must be created by combining one or more paths.

- Drawing paths
    1. Create a path
    2. use drawing commands to draw into the path
    3. once created stroke or fill the path to render it
        - beginPath() creates new path

**bottom line** this page shows different methods for drawing geometric shapes with canvas, two above being the two primitive shapes. 

# Applying style and color
    - lots of information here.  I have bookmarked
    **bottom line** - color and transparency can be used in canvas will fillstyle and stroke style.  Lots of info here to reference

# Drawing text
    - two methods for rendering text
        - fillText(text, x, y [, maxWidth])
- Styling text
    - font = value
    - textAlign = value
    - textBaseline = value
    - direction = value

- Advanced text measurments
    - measureText()
        - returns a **TextMetrics** object containing width that the specified text will be when drawn
        


