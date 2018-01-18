!!! note "Description"
    API v1 is RESTful API for Java daemon. Extend it only if you are adding new functionality to the daemon or modifying/fixing existing processes. Check the [flow scheme](../assets/rest_flow_2017-03-29.png) if Java is strong in you.

* **Response format:** JSON
* **Sessions:** none

# Authentication

* HttpBasicAuth<br>
  Basic HTTP authentication, login and password are transferred as a string `login:password`<br><br>
* HttpBearerAuth<br>
  Token based authentication. To use it, you should pass bearer token in the HTTP header:

        header('Authorization: Bearer USER_TOKEN');

* QueryParamAuth<br>
  Works in the same manner as HttpBearerAuth (i.e. identifies user with its token), but in this case token is passed as GET parameter
     
        http://SITE_NAME/index.php?r=v1/core/ACTION_NAME&token=USER_TOKEN

# Class hierarchy

v1 module controllers can extend `yii\rest\ActiveController` or `yii\rest\Controller` depending on what is necessary. `ActiveController` allows us to manage certain model without redefining get-set methods (we're using Yii2 magic). If you need custom controller, extend `yii\rest\Controller` and do some manual labor.

# REST request methods

_Method_ | _Description_
------------ | -------------
GET | get data
PUT | edit data
DELETE | delete data
POST | create data

# REST response codes

_Code_ | _Description_
------------ | -------------
200 | Success + DATA (GET SUCCESS, PUT SUCCESS)
201 | Created + DATA (POST SUCCESS)
204 | Operation success, but no responce + NO DATA (DELETE SUCCESS)
404 | Not Found + NO DATA (GET, PUT, DELETE - NOT FOUND)
422 | Unprocessable Entity + NO DATA (GET, PUT, POST VALIDATION FAILED OR REQUIRED PARAMETER MISSING OR EMPTY). It's not related to missing GET parameter - system will return 400.
500 | Internal Server Error + NO DATA (GET, PUT, POST, DELETE - DB ERROR)

# Test v1 API via CLI

```bash
// simple test, where -i tells to retrieve headers with data
$ curl -i -H "Accept:application/json" "http://localhost/index.php?r=v1/core/isalive"

// Simple call without headers
curl -H "Accept:application/json" "http://localhost/index.php?r=v1/core/isalive" 

// With authentication
curl -i -H "Accept:application/json" --user admin:admin "http://localhost/index.php?r=v1/core/isalive" 
```
