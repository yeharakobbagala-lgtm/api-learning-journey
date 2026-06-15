**1. API Request Components**



When Postman sends a request, it can contain:



Headers



Extra information (metadata) sent with the request.



Examples:



Content-Type: application/json

Accept: application/json

Authorization: Bearer token123

User-Agent: Postman



In Postman:



Open Headers tab

Enter:

Key

Value

Enable checkbox

Query Parameters



Used for filtering, searching, sorting, etc.



Example:



https://example.com/api/users?age=25\&city=London



Meaning:



age = 25

city = London



In Postman:



Open Params tab

Add:

Key	Value

age	25

city	London



Postman automatically builds:



?age=25\&city=London





**2. Request Body**



Data sent to the server.



Usually used with:



POST

PUT

PATCH

Raw JSON



Most common API format.



{

&#x20; "name": "John",

&#x20; "email": "john@gmail.com"

}



Postman



Body

↓

raw

↓

JSON

Form Data



Sent as key-value pairs.



name = John Doe

email = john@gmail.com



Mostly used for:



File uploads

Images

PDFs

Documents

URL Encoded



Looks like:



name=John\&email=john@gmail.com



Used mostly by older systems and web forms.



**3. Authentication**



Authentication proves who you are.



Basic Auth



Uses:



Username

Password



Example:



admin

secret123



Postman



Authorization

↓

Basic Auth

↓

Username

Password

Bearer Token



Modern APIs usually use Bearer Tokens.



Example:



Authorization: Bearer abc123xyz



Postman



Authorization

↓

Bearer Token

↓

Paste token



Common token types:



JWT Token

OAuth Token



**4. Environment Variables**



Environment variables are like labeled boxes that store values.



Instead of writing:



https://api-learning.nisalgunawardhana.com



everywhere,



store it as:



base\_url



Value:



https://api-learning.nisalgunawardhana.com



Then use:



{{base\_url}}/api/users



Postman replaces:



{{base\_url}}



with:



https://api-learning.nisalgunawardhana.com



automatically.



Development vs Production

Development



While building and testing.



http://localhost:3000



Meaning:



My own computer



Example:



{{base\_url}}/api/users



becomes



http://localhost:3000/api/users

Production



After deployment.



Example:



https://myapp.com



or



https://api-learning.nisalgunawardhana.com



Same request:



{{base\_url}}/api/users



becomes



https://api-learning.nisalgunawardhana.com/api/users



Only the environment changed.



The request stayed the same.



API Token Variable



Instead of writing:



Authorization: Bearer abc123xyz



every time,



store:



api\_token = abc123xyz



Then:



Authorization: Bearer {{api\_token}}

User ID Variable



Store:



user\_id = 25



Use:



{{base\_url}}/api/users/{{user\_id}}



Postman converts it to:



https://api-learning.nisalgunawardhana.com/api/users/25



**5. Scripts**



There are two types.



Pre-request Script



Runs BEFORE sending request.



Example:



pm.environment.set(

&#x20; "timestamp",

&#x20; new Date().toISOString()

);



Meaning:



Step 1



Get current date and time.



new Date()

Step 2



Convert to standard format.



toISOString()



Example result:



2026-06-15T10:30:00.000Z

Step 3



Save it as:



timestamp



environment variable.



Test Script (Post-response Script)



Runs AFTER receiving response.



Example:



pm.test("Status code is 200", function () {

&#x20;   pm.response.to.have.status(200);

});



Meaning:



Test name

"Status code is 200"

Check

pm.response.to.have.status(200);



Verify server returned:



200 OK



If yes:



PASS ✅



Otherwise:



FAIL ❌

Check Response Data

pm.test("User has name", function () {

&#x20;   var jsonData = pm.response.json();



&#x20;   pm.expect(jsonData)

&#x20;     .to.have.property("name");

});



Meaning:



Convert response into JSON.



var jsonData = pm.response.json();



Check if:



name



exists.



Example:



{

&#x20; "name": "John"

}



PASS ✅



Save Response Data

var jsonData = pm.response.json();



pm.environment.set(

&#x20;   "user\_id",

&#x20;   jsonData.id

);



Example response:



{

&#x20; "id": 25,

&#x20; "name": "John"

}



Postman saves:



user\_id = 25



Now you can use:



{{user\_id}}



in future requests.

