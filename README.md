# zell-rest-api

## Quick notes from Zell's article from Smashing Magazine:
## Understanding and Using REST API's
https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/




### API stands for application programming interface
  it is a set of rules that allow programs to talk to eachother (or as Leon says, a menu)
  Developer creates the API on the server, and allows the client to talk to it (REMEMBER MVC)
  
### REST - Representational state Transfer
  determines the look of the API. 
  set of rules developers follow when creating API
  One rule states you should be able to get a piece of data (a RESOURCE) when you link to a specific URL
  each URL is called a REQUEST  
  data sent back is RESPONSE
  

### Anatomy of a Request:
   - Requests have four things:
          1 - Endpoint
          2 - Method
          3 - Headers
          4 - Data (or body)
          
        ###  1 - ENDPOINT (or route) 
          - the URL you request for. looks like: root-endpoint/?
              ROOT (not to be confused with route) endpoint is starting point of API we are requesting                from. (ex: https://api.github.com or https://api.twitter.com
              PATH determines resource we're requesting for. (Answering machine metaphor - 1 for service, 2 for another, etc)
              
          PATHS can be accessed just like linking parts of websites.  Example: www.smashingmagazine.com/tag/javascript
          www.smashingmagazine.com/ is the root-endpoint and /tag/javascript is the path
          
          Which paths are available? read API documentation.
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

           
              
