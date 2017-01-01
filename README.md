# SimpleIssueTracker-token-based-RESTFul-

Following things are implemented:
###i.   Every endpoint need user authentication -->complete
###ii.  Authentication should be stateless (access_token) -->complete
###iii. User who created the issue only should be able to edit or delete that issue -->complete
####iv. Whenever an Issue is created or assigned to different user(in case of update), 
####an email should be triggered exactly after 12 mins to the particular user saying issue has been assigned to him/her.
####-->partially,as email is triggered immediately not after 12 min for hardcoded case only.i.e if the sender is "amol.3793@gmail.com"


**1. GET  "/users" or "/" --> will give all register user  (no login required)**

**2. POST  "/users" ---> will Create a user   (no login required)**

Body for creating user -->no "accesstoken" field as i am not using that field in my implementation,as i am using "itsdangerous" module which takes care of token
                       -->Assuming that if all below 5 fields are provided then only issue will be created
{
"email" : "123@gmail.com",
"username" : "123",
"firstname": "123",
"lastname": "123",
"password": "123"
}

**3.GET "/users/<int:id>"--> details of  user whoese id is provided -->(no login required)**

**4.PUT "/users/<int:id>"--> modify the user with only the details which are provided in the body-->(no login required)**

Body can be as follows:
case1
{
"email" : "123@gmail.com"
}

case2
{
"email" : "123@gmail.com",
"firstname": "123",
"lastname": "123",
"password": "123"
}

**5.DELETE "/users/<int:id>" ---> will delete the user whoese ID is provided (no login required)**

**6. GET "/issues"--> will return all the issues (no login required)**



###For token based flow:
####step1: GET "/token" (login required)
####step2: Enter your credentials in username and password field
####Step3: a token will generate and save that token and use that token in each request in "username field" of authentication(password can be blank /or anything as I'm not considering)
####step4: all the login_required endpoints can be accessed using that access token
###NOTE: each token has expiry time of 10min,so have to get new tocken after 10 min.



**7. POST "/issues/create"--> will create issue  (login required)**

Body for creating Issue->Assuming that if all below 4 fields are provided then only issue will be created
"createdby" will be added automatically by login user id

{
"title":"issue1",
"description" :"description for 1",
"assignedto" : "1",
"status":"open"
}

**8. GET "/issues/<int:id>"--> will give details of the issue whoese id is provided (login required)**

**9. PUT "/issues/<int:id>"-->modify the issue (login required)**

Note: "createdby" and "id" can not be changed,And only the creator of the issue can modify

Body for PUT can be:
case1
{
"title":"issue1",
"description" :"description for 1",
"assignedto" : "1"
"status":"open"
}

case2
{
"status":"CLOSE"
}

etc.

**10. DELETE "/issues/<int:id>"-->delete  the issue (login required)**

NOTE: only creater of the issue can delete the issue.










