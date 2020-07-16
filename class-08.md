# The Past, Present & Future of Local Storage for Web Applications
* Native applications/operating systems typically provide storing capacity for app specific data.  Web applications don't have this luxury.  Issue solved with cookies but they have downsides including slowing down web app and limited data of 4kb

* A brief history of local storage hacks before HTML5
    - userData allowed web pages to store up to 64kb of data per domain. 
    - 2002 Adobe introduced flash allowing up to 100KB per domain
    - 2006 Google launched open source browser Gears.  Provides API to embedded SQL database

* HTML5 storage 
    - web storage.  
    - web pages store named key/value pairs locally within browser.  They persist after you navigate away from page but are never transmitted

* Using HTML5 storage
    - based on key/value pair
    - data is stored in a string
    - uses local storage

* Beyond named Key-Value Pairs: Competing Visions
    - Web SQL Database provides thin wrapper around SQL database
