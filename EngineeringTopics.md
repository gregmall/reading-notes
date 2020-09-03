# Quantity Trumps Quality
* Coding is best learned by writing lots and lots of code
- Good, bad and ugly code all helps to understand what it is you are writing when it comes to code. Learning from mistake is a valuable takeaway. 
- Like learning to paint, you don't start by painting the Mona Lisa.  You might finger paint and practice techniques until you hone the skills to paint a masterpiece.  Coding is much like this.
* Stop Theorizing
- prove your ideas by implementing them in real applications that will be used by actual users
* Write lots of code
- the only way to get better at writing code is to WRITE CODE   
* Learn from your mistakes
- software development is difficult. You should always be failing some of the time and learning from those failures. 

# Clean Code CHAPTER 1
* There will be code
- the level of abstraction of code will grow but it will not eliminate code.
- code is the language in which we express requirements
* Bad Code 
- bad code can ultimately be the death nail of an app.  
- 'wading' is the term for slogging through bad code that can be a pile of tangled branches and hidden pitfalls without seeing anything but senseless code.
- bad code can be the result of trying to rush/go to fast 
* The Total Cost of Owning a Mess
- teams moving faster writing code early on often find themselves moving at a snail's pace later on
- later additions and modifications can break other parts of earlier code and must be tracked down and understood, slowing progress
- as this mess builds, productivity can slow to almost a stop.  Often management tries to solve this by hiring more staff to the programming team which inevitably adds to the problem.  
* The Grand Redesign in the Sky
- when code becomes too odious, the team eventually rebels and demands a grand redesign.  
- a second team is formed to create the redesign but the original team must stay in place to maintain the current system until the new design can take over.
- this can take years
- in the end the original team can demand that the NEW system be redesigned because it too is a mess
* Attitude
- programmers must let managers know that timelines and features cannot be more important than writing good, clean code. 
* The Primal Conundrum
- programmers know that previous messes slow them down however they feel the pressure to make messes in order to meet deadlines
- fact: you will NOT make the deadline by making the mess.  They only way to make the deadline is to keep the code as clean as possible
* The Art of Clean Code
- being able to recognize clean code from dirty code does not mean we know how to write clean code.
- requires 'code-sense'; choosing the best variation and guide them to plot a sequence of behavior preserving transformations to get from here to there
* What Is Clean Code?
- Bjarne Stroustrup
    - "I like my code to be elegant and efficient. The logic should be straightforward to make it hard for bugs to hide, the dependencies minimal to ease maintenance, error handling complete according to an articulated strategy, and performance close to optimal so as not to tempt people to make the code messy with unprincipled optimizations. Clean code does one thing
    well."
    - efficiency
    - elegant
    - error handling complete
- Grady Booch
    - "Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer’s intent but rather is full of crisp abstractions and straightforward lines of control."
    - readability
    - crisp abstraction
- Dave Thomas
    - "Clean code can be read, and enhanced by a developer other than its original author. It has unit and acceptance tests. It has meaningful names. It provides one way rather than many ways for doing one thing. It has minimal dependencies, which are explicitly defined, and provides a clear and minimal API. Code should be literate since depending on the language, not all necessary information can be expressed clearly in code alone."
    - cleanliness tied to tests
    - minimal
    - literate
- Michael Feathers
    - "I could list all of the qualities that I notice in clean code, but there is one overarching quality that leads to all of them. Clean code always looks like it was written by someone who cares. There is nothing obvious that you can do to make it better. All of those things were thought about by the code’s author, and if you try to imagine improvements, you’re led back to where you are, sitting in appreciation of the code someone left for you—code left by someone who cares deeply about the craft."
    - care
- Ron Jeffries
    - "In recent years I begin, and nearly end, with Beck’s rules of simple code. In priority order, simple code:
        • Runs all the tests;
        • Contains no duplication;
        • Expresses all the design ideas that are in the system;
        • Minimizes the number of entities such as classes, methods, functions, and the like
    Of these, I focus mostly on duplication. When the same thing is done over and over, it’s a sign that there is an idea in our mind that is not well represented in the code. I try to figure out what it is. Then I try to express that idea more clearly. Expressiveness to me includes meaningful names, and I am likely to change the names of things several times before I settle in. With modern coding tools such as Eclipse, renaming is quite inexpensive, so it doesn’t trouble me to change. Expressiveness goes The  beyond names, however. I also look at whether an object or method is doing more than one thing. If it’s an object, it probably needs to be broken into two or more objects. If it’s a method, I will always use the Extract Method refactoring on it, resulting in one method that says more clearly what it does, and some sub methods saying how it is done. Duplication and expressiveness take me a very long way into what I consider clean code, and improving dirty code with just these two things in mind can make a huge difference. There is, however, one other thing that I’m aware of doing, which is a bit harder to explain. After years of doing this work, it seems to me that all programs are made up of very similar elements. One example is “find things in a collection.” Whether we have a database of employee records, or a hash map of keys and values, or an array of items of some kind, we often find ourselves wanting a particular item from that collection. When I find that happening, I will often wrap the particular implementation in a more abstract method or class. That gives me a couple of interesting advantages. I can implement the functionality now with something simple, say a hash map, but since now all the references to that search are covered by my little abstraction, I can change the implementation any time I want. I can go forward quickly while preserving my ability to change later. In addition, the collection abstraction often calls my attention to what’s “really” going on, and keeps me from running down the path of implementing arbitrary collection behavior when all I really need is a few fairly simple ways of finding what I want. Reduced duplication, high expressiveness, and early building of simple abstractions. That’s what makes clean code for me. Here, in a few short paragraphs, Ron has summarized the contents of this book. No duplication, one thing, expressiveness, tiny abstractions. Everything is there. "
    
- Ward Cunningham
    - " You know you are working on clean code when each routine you read turns out to be pretty much what you expected. You can call it beautiful code when the code also makes it look like the language was made for the problem."
    
* Boy Scout Rule
- not enough to just write clean code.  Code must be kept clean over time.
* Conclusion
- you cannot become an artist by reading a book.  A book can give you tools and teach techniques but cannot make you an artist.  Practice, practice, practice.

# TDD Red, Green, Refactor
* TDD is an approach to software development where you test first then use the tests to drive design and development
* RED, GREEN, REFACTOR
- Red: think about what you need to develop
- Green: think about how to make your tests pass
- Refactor: think about how to improve existing implementation
* RED
- starting point
- write the test that informs implementation of a feature
* GREEN
- implement code to make test pass
- goal is to find a solution
* REFACTOR
- think about how to implement code better or more efficiently
- accomplish the same output with more descriptive or faster code
- questions to consider when refactoring:
    - Can I make my test suite more expressive?
    - Does my test suite provide reliable feedback?
    - Are my tests isolated?
    - Can I reduce duplication in my test suite?
    - Can I make my implementation code more descriptive?
    - Can I implement something more efficiently?
* Conclusion
- using red, green, refactor TDD to approach large software implementation problems will save time while implementing a more robust solution.

# Cycles of TDD
* Second by Second
- Three Laws of TDD:
    1. You must write failing test before you write any production code
    2. You must not write more of a test than is sufficient to fail
    3. YOu must not write more production code than is sufficient to make the currently failing test pass.
    - nano-cycle of TDD
* Minute by Minute
- Rules of the RED/GREEN/REFACTOR cycle:
    1. Create a unit test that fails.
    2. Write production code that makes that test pass
    3. Clean up the mess you just made
    - make it work, make it right, make it fast
    - getting software to work is only half the job
- customers value 2 things about software:
    - the way it makes a machine behave
    - the ease in which it can be changed
* Decaminute by Decaminute
- as the tests get more specific, the code gets more generic
- programmers make specific cases work by writing code that makes the general case work
- without the big picture the developer cannot imbue the software with the correct structure for the overall problem
- to avoid getting stuck we evaluate our position every few minutes
* Hour by Hour
- final cycle ensures that all the other cycles are driving towards a clean architecture.
- every hour or so we stop and look at the overall system and make decisions about boundaries and constraints. 




