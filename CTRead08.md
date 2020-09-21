# HTTP:  The Protocol Every Wb Developer Must Know
* HTTP - Hypertext Transfer Protocol.
    - stateless
## HTTP Basics
- HTTP allows for communication between a variety of hosts and clients, and supports a mixture of network configurations.
- communication corrurs via **request/response pair**
**URLs**
- Uniform Resource Locators
  !(/assets/http1-url-structure.png)

**Verbs**

- Request Verbs:
    - **GET:** - fetch an existing resource
    - **POST:** - create a new resource
    - **PUT:** - update an existing resource
    - **DELETE:** - delete an existing resource
- Lesser Verbs:
    - **HEAD:** - similar to GET but without the message body
    - **TRACE:** - retrieves the hops that a request takes to round trip from the server.
    - **OPTIONS:** - used to retrieve the server capabilities

**Status Codes**
- code that tells the client how to interpret server response
- **Informational Messages**
    - Expect: 100-continue
- **Successful**
    - **202** - Accepted
    - **204** - No Content
    - **205** - Reset Content
    - **206** - Partial Content
- **Redirection**
- requires the client to take additional action
    - **301** - Moved Permanently
    - **303** - See Other
    - **304** - NOt Modified
- **Client Error**
- when server thinks it is client fault
    - **400** - Bad Request
    - **401** - Unauthorized
    - **403** - Forbidden
    - **405** - Method Not Allowed
    - **409** - Conflict
- **Sever Error**
- server failure while processing the request
    - **501** - NOt Implemented
    - **503** - Service Unavailable

** Request and Response Message Formats
!(/assets/http1-req-res-details.png)

- **General Headers**
- general headers are shared by both request and response messages
    - Via : used in TRACE message. Updated by intermittent Proxies and gateways
    - Pragma : custom header may be used to include implementation specific headers
    - Date : timestamp the request/response message
    - Upgrade : switch protocols and allow transition to a newer protocol
    - Transfer-Encoding : Break the response into smaller parts
- **Entity Headers**
-  messages may also include entity headers to provide meta-information about the the content 
- **Request Format**
- has the same generic structure as Entity Headers

- **Response Format**
- status lines are different from above formats

## Tools to View HTTP Traffic

- Chrome/Webkit inspector
- Fiddler : for Windows
- Charles Proxy : for OSX

## Using HTTP in Web Frameworks and Libraries

* ExpressJS
- NodeJs
- Sample of API requests:
    - req.body: get the request body.
    - req.query: get the query fragment of the URL.
    - req.originalUrl
    - req.host: reads the Host header field.
    - req.accepts: reads the acceptable MIME-types on the client side.
    - req.get OR req.header: read any header field passed as argument.
- Sample of responses: 
    - res.status: set an explicit status code.
    - res.set: set a specific response header.
    - res.send: send HTML, JSON or an octet-stream.
    - res.sendFile: transfer a file to the client.
    - res.render: render an express view template.
    - res.redirect: redirect to a different route. Express automatically adds the   default redirection code of 302.

* Ruby on Rails
- **ActionController** - provides a high level API to read the request URL, render output and redirect to a different end-point
- methods are as follows:
    - params: gives access to the URL parameters and POST data.
    - request: contains information about the client, headers and URL.
    - response: used to set headers and status codes.
    - render: render views by expanding templates.
    - redirect_to: redirect to a different action-method or URL.
- **ActionDispatch**
- fine-grained access to the request/response messages 

* JQuery Ajax
- Ajax API provides the opposite of server-side framework.  Allows you to read response messages and modify request messages.













