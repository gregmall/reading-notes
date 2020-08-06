# URLSearchParams built-in class
**The URLSearchParams interface defines utility methods to work with the query string of a URL.**
* Constructor
    - Returns a URLSearchParams object instance.
* Methods 
    - URLSearchParams.append()
        - Appends a specified key/value pair as a new search parameter.
    - URLSearchParams.delete()
        -Deletes the given search parameter, and its associated value, from the list of all search parameters.
    - URLSearchParams.entries()
        - Returns an iterator allowing iteration through all key/value pairs contained in this object.
    - URLSearchParams.forEach()
        - Allows iteration through all values contained in this object via a callback function.
    - URLSearchParams.get()
        - Returns the first value associated with the given search parameter.
    - URLSearchParams.getAll()
        - Returns all the values associated with a given search parameter.
    - URLSearchParams.has()
        - Returns a Boolean indicating if such a given parameter exists.
    - URLSearchParams.keys()
        - Returns an iterator allowing iteration through all keys of the key/value pairs contained in this object.
    - URLSearchParams.set()
        - Sets the value associated with a given search parameter to the given value. If there are several values, the others are deleted.
    - URLSearchParams.sort()
        - Sorts all key/value pairs, if any, by their keys.
    - URLSearchParams.toString()
        - Returns a string containing a query string suitable for use in a URL.
    - URLSearchParams.values()
        - Returns an iterator allowing iteration through all values of the key/value pairs contained in this object.

# toString() returns query string
**The toString() method of the URLSearchParams interface returns a query string suitable for use in a URL.**
* Syntax: URLSearchParams.toString()
    - no parameters
    - returns a DOMString without the question mark.

# Built-in Location Object
**The Location interface represents the location (URL) of the object it is linked to.**
    - Changes done on it are reflected on the object it relates to.
    - Both the Document and Window interface have such a linked Location, accessible via Document.location and Window.location respectively.

* Properties 
    - Location.ancestorOrigins
        -Is a static DOMStringList containing, in reverse order, the origins of all ancestor browsing contexts of the document associated with the given Location object.
    - Location.href
        - Is a stringifier that returns a USVString containing the entire URL. If changed, the associated document navigates to the new page. It can be set from a different origin than the associated document.
    - Location.protocol
        -Is a USVString containing the protocol scheme of the URL, including the final ':'.
    - Location.host
        - Is a USVString containing the host, that is the hostname, a ':', and the port of the URL.
    - Location.hostname
        - Is a USVString containing the domain of the URL.
    - Location.port
        - Is a USVString containing the port number of the URL.
    - Location.pathname
        - Is a USVString containing an initial '/' followed by the path of the URL.
    - Location.search
        - Is a USVString containing a '?' followed by the parameters or "querystring" of the URL. Modern browsers provide URLSearchParams and URL.searchParams to make it easy to parse out the parameters from the querystring.
    - Location.hash
        - Is a USVString containing a '#' followed by the fragment identifier of the URL.
    - Location.origin Read only
        - Returns a USVString containing the canonical form of the origin of the specific location.
* Methods
    - Location.assign()
        - Loads the resource at the URL provided in parameter.
    - Location.reload()
        - Reloads the current URL, like the Refresh button.
    - Location.replace()
        - Replaces the current resource with the one at the provided URL (redirects to the provided URL). The difference from the assign() method and setting the href property is that after using replace() the current page will not be saved in session History, meaning the user won't be able to use the back button to navigate to it.
    - Location.toString()
        - Returns a USVString containing the whole URL. It is a synonym for HTMLHyperlinkElementUtils.href, though it can't be used to modify the value.

# Hash change event

**The hashchange event is fired when the fragment identifier of the URL has changed (the part of the URL beginning with and following the # symbol).**
