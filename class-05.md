# Chapter 5 HTML/CSS Images
* images- between empty emement <img>
    - src tells browser where to find
    - alt is text description if image can't be loaded/found
    - title attribute can be used with the img element to provide additional info
    - height in pixels
    - width in pixels
* aligning images
    - horizontal with left and right
    - vertical with top/middle/bottom
* 3 Rules for creating images
    - save image in the right format
    - save image at the right size
    - measure image in pixels

**Images should be saved at the same width/height that you want them to appear**

* <figure> element contains images and their captions so that the two are associated
* <figcaption> allows we page authors to add a caption to an image
*  Photos are better saved as JPEG
* Logos and illustrations are best saved as GIF

# Chapter 11 HTML/CSS Color

* RGB values
    -red, green, blue.  ex rgb(100,100,90)

* HEX codes
    - six-digit code that represents amout of red/green/blue

* Color names
    - 147 (probably more now) predefined colors in CSS

* Background color 
    -set the backgound color for the box
    -often set in <body>

* Contrast
    - Low contrast
        - Test is harder to read
    - High contrast
        - test is easer to read
    - Medium contrast
        - for long spans it improves readability of text
* Opacity
    - value is a number between 0.0 and 1.0 

* Hue
    - expressed as an angle (between 0 and 360 degrees)

* Saturation 
    - expressed by percentage

* Lightness
    - percentage (0% being white, 50% being normal, 100% being black)

* Alpha
    - number between 0 and 1.0

# Chapter 12 HTML/CSS Text

* Properties that allow you to control the appearence of text split into 2 groupes:
    - those that dirctly affect the font and its appearance
    - those that would have the same effect on text no matter what font you were using


* font-face
    - CSS specifies where it can be downloaded if not installed on the computer
    - downloaded to the font file
* service-based-font-face
    - commercial services give users access to a wider range of fonts
    - ongoing fee to pay for usage
* images
    - create a graphic that contains the text as you want it to appear
    - people with screen readers will rely on alt text to know what is said
* sifr
    - font is embedded into a flash movie
    - only works if user has flash and javascript enabled
* cufon
    - uses javascript to create either a svg or vml version of the text
    - requires javascript to be enabled.  Users cannot select text. Cant change with 
      hover.

* font-family
    - CSS used to specify the typeface
    - limited choice
    - allows you to specify the typeface that should be used
    - value is the name of the typeface
    - can list fonts so that if user doesn't have first choice installed it goes to 
      next font on the list

* font-size
    - enables you to specify a size for the font
    - can be in pixels, percentages or ems

* @font-face
    - allows you to use a font even if not installed on the computer
    - a path is provided to the computer to a copy of the font to be downloaded

* font-weight
    - **BOLD** 
    - normal
* font-style
    - normal
    - italic
    - oblique

* text-transform
    - **uppercase** causes text to appear uppercase
    - **lowercase** ... ... ... .... .... lowercase
    - **capitalize** first letter of each word appears capitalized

* text-decoration
    - **none** removes any decoration already applied
    - **underline** add a line underneath the text
    - **overline** adds a line over the top of the text
    - **line-through** adds a line through the word
    - **blink** animates the text to flash on and off

* text-align
    - left
    - right
    - center
    - justify  every line in paragraph will take up the full width of box

* vertical-align
    - commonly used inline elements
    - baseline
    - sub
    - super
    - top
    - text-top
    - middle
    - bottom
    - text-bottom

* text-indent
    - allows you to indent the first line of a text within an element
        - usualy given in pixels

* text-shadow
    - creates a dark verson of the word just behind and slightly offset
    - takes 3 lengths
        1.  how far to the left or right shadow should fall
        1.  distance to the top or bottom and the shadow should fall
        1.  amount of blur that should be applied (optional)
        1.  color of shadow

* first-letter, first-line
    - set different values for the first letter or first line of text in an element  

* link, visited
    - **link** allwos you to set sylte for links not yet visited
    - **visited** allows you to set sytle for links that have been clicked on

* hover, active, focus
    - **hover** transforms text when hovered over with pointer
    - **active** applied when an element is being activated
    - **focus**  applied when an element has focus
        - occurs when a browser descovers that you are ready to interact with an     element on the page.

* attribute selectors
    - **EXISTENCE** [] matches a specific attribute
    - **EQUALITY** [=] matches a specific attribute with specific value
    - **SPACE** [~=] matches specific attritube whose value appears in a space separated list of words
    - **PREFIX** [^=}]  matches a specific attribute whose value begings with a specific string
    - **SUBSRING** [*=]  Matches a specific attribute whose value contains a specific substring
    - **SUFFIX** [$=]  Matches a specific attribute whose value ends with a specific string





























