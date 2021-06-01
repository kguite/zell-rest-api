# zell-rest-api

## Quick notes from Zell's article from Smashing Magazine:
 Understanding and Using REST API's
https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/




### API: Application Programming Interface
  it is a set of rules that allow programs to talk to eachother (or as Leon says, a menu)
  Developer creates the API on the server, and allows the client to talk to it (REMEMBER MVC)
  
### REST: Representational State Transfer
  determines the look of the API. 
  set of rules developers follow when creating API
  One rule states you should be able to get a piece of data (a RESOURCE) when you link to a specific URL
  each URL is a REQUEST  
  data sent back is RESPONSE
  

### Anatomy of a Request:
   - Requests have four things:
          1 - Endpoint
          2 - Method
          3 - Headers
          4 - Data (or body)
          
        ###  1 - ENDPOINT (or route) 
          - the URL you request for. it looks like: root-endpoint/?
              ROOT (not to be confused with route) endpoint is starting point of API we are requesting                from. (ex: https://api.github.com or https://api.twitter.com
              PATH determines resource we're requesting for. (Answering machine metaphor - 1 for service, 2 for another, etc)
              
          PATHS can be accessed just like linking parts of websites.  Example: www.smashingmagazine.com/tag/javascript
          www.smashingmagazine.com/ is the root-endpoint and /tag/javascript is the path
          
          Which paths available? read API documentation.
          Github example: the docs say to get a list of repositories by a certain user, use /users/:username/repos
          
          COLONS: any : on a pth denotes a variable. REPLACE these with actual values when you send your request (example above, change username to the actual one you're searching for).
          
          That would change the endpoint: https://api.github.com/users/zellwk/repos
          
          QUERY PARAMETERS: give you the option to modify your request with key-value pairs.
                (not technically a part of the REST architecture, but many API's use them)
               ?  Always begin with a question mark
               & separated with an ampersand
               like this: ?query1=value1&query2=value2
               
               Example: when trying to get a list of a user's repositories on github, you add three possible paramters to the request to modify the results given to you.
               
               
               
 <img width="513" alt="Screen Shot 2021-04-08 at 12 18 07 PM" src="https://user-images.githubusercontent.com/33885541/114083947-7b6fad00-9864-11eb-9c20-d70a0438c258.png">

           To get a list of repos that Zell pushed to recently, can set "sort" to "push", like this: https://api.github.com/users/zellwk/repos?sort=pushed

           
    - Testing Endpoints with Curl:
            Requests can be made with any programming language
            JavaScript uses methods like the FetchAPI and jQuery's Ajax Method
            
    - cURL is a command line utility.
           API documentations normally written with reference to cURL
           check cURL is installed with curl --version (mine is 7.64.1)
           
    - To use cURL:
          Type curl followed by the endpoint you're requesting for.
          example: curl https://api.github.com
          response should look like this:
          
 <img width="539" alt="Screen Shot 2021-04-08 at 1 44 39 PM" src="https://user-images.githubusercontent.com/33885541/114093947-921c0100-9870-11eb-9688-fb99ee387dea.png">


          To get a list of a user's repositories, modify the endpoint:
            example: curl https://api.github.com/users/zellwk/repos
          
          
          To include query parameters with cURL:
              Make sure to prepend a / BEFORE the ? and = characters.
                 Because ? and = are special characters in command line. need to                    use / before them for command line to interpret them as normal                      characters.
                 Example: curl https://api.github.com/users/zellwk/repos\?sort\=pushed
           
  
  
  ### JSON: JavaScript Object Notation
            - a common format for sending and requesting data through a REST API.
            - the repsonse Github sends back is formatted as JSON
            - JSON looks like Javascript Object.
            - JSON properties AND values must be wrapped with DOUBLE quotation marks (and don't forget the commas)

  <img width="529" alt="Screen Shot 2021-04-08 at 1 59 22 PM" src="https://user-images.githubusercontent.com/33885541/114095735-a103b300-9872-11eb-9860-3bca21a5f1d9.png">


   ###  2 - METHODS 
         Method is type of request sent to the server.
         Five Types of methods:
            1. GET
            2. POST
            3. PUT
            4. PATCH
            5. DELETE

          Methods used to perform four possible actions:
            1. CREATE
            2. READ
            3. UPDATE
            4. DELETE
            
   
 <strong>GET METHOD:</strong> used to get a resource from a server.  GET request tells the server to look for the data you requested and sends it back to you.  
     
 <strong>a GET request performs a "READ" operation.  GET is the DEFAULT request method.</strong>
    
 <strong>POST METHOD:</strong> used to create a new resource on a server.  The server creates a new entry in the database and tells you whether the creation is successful.
    
<strong>a POST request performs a "CREATE" operation</strong>
     
<strong>PUT AND PATCH METHOD:</strong> used to update a new resource on a server.  If you perform a  PUT or PATCH requst, the server updates an enetry in the database and tells you whether the update is successful.  
    
<strong>a PUT OR PATCH request performs an "UPDATE" operation</strong>                 
<strong>DELETE:</strong> used to delete a resource from a server.  If you perform a  PUT or PATCH requst, the server updates an enetry in the database and tells you whether the update is successful.  
    
<strong>a DELETE request performs a "DELETE" operation</strong>                                  


        The API lets you know which request method to use each request.  For example, to get a list of a user's repositories, you need a GET request:
        GET /users/:username/repos
        
        To create a new Github repository, you need a POST request:
        POST /user/repos
        
        
       How to set request method in cURL?
          Write -x or --request followed by the request method.
          example: curl -X POST https://api.github.com/user/repos
          
          
   ###  3 - HEADERS 
         - Headers are property-value pairs that are separated by a colon.
         - example: "Content-Type: application/json"

         - Headers are used to provide info to both client and server.  Authentication, info about the body conent, etc.  
         - More info here: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers

        - Can send HTTP headers with curl throgugh the -H or --header options
        - example: curl -H "Content-Type: application/json" https://api.github.com
        - Note: content-type header is not a requirement for Github's API tow ork, it's just an example of how to use a header with cURL)
        
        - To view headers you've sent:
        - use the -v or --verbose option as yo usend the request:
        - example: curl -H "Content-Type: application/json" https://api.github.com -v

<img width="553" alt="Screen Shot 2021-04-08 at 2 20 53 PM" src="https://user-images.githubusercontent.com/33885541/114098015-a282aa80-9875-11eb-96e4-49c77b31b1c6.png">
        Here, * refers to additional information provided by cURL. > refers to request headers, and < refers to the response headers.
        
        
   ###  3 - DATA or BODY:
        
