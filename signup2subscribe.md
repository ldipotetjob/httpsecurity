## This document is refered to Restful WSO2 api manager ##

Our goals: 
- Make a sign up 
- This new user has to be capable of:
  - add new applications 
  - subcribe to new Apis
  
### Sign up: ###
  
 ```sh
 curl 'http://localhost:9763/store/site/blocks/user/sign-up/ajax/user-add.jag' -H 'Accept: application/json' -d 'action=addUser&username=myusername&password=PyPassword1&allFieldsValues=Kim|Hill|ABC Network|30 Palm Road,Pasadena,California|USA|kim@abcnetwork.com|0016269934122|0016269934134|kimhill|www.abcNsounds.org/'
 ```
 Some details about previous curl command:
 - password ,ost be a combination of uppercases,lowercase and digits. checke this point in WSO2 documentation. 
 - **allFieldsValues** parameter is **mandatory** if you do not need all of then leave empty as explain in the next parameters.  
 - be prepared for this response:
   - {"error" : false, "showWorkflowTip" : false} : means everything ok. In the same way when something is wrong responses can be ambiguous or lead confusion.
 - If want to be prepared for all responses:
   - *<WSO2_HOME>/repository/deployment/server/jaggeryapps/store/site/blocks/user/sign-up/ajax/user-add.jag*
   
  Sign up with just few info(**pay attention to the module bar(|)**):

```sh
  curl 'http://localhost:9763/store/site/blocks/user/sign-up/ajax/user-add.jag' -H 'Accept: application/json' -d 'action=addUser&username=myusername&password=PyPassword1&allFieldsValues=Kim|Hill|ABC Network|||myemail@mail.com||||'
```
 
 [In this website all content is deprecated with the exception of Sign up rest service.](https://docs.wso2.com/display/AM200/Store+APIs#StoreAPIs-UserSignup)
  
### Add new applications: ###

The workflow when you create an application in WSO2 is quite different when it is done via web console than or when it is done by Restful api.

It it not clear in the documentation. So we have a reference, there is a document that explain [RestFull api for deal with WSO2](https://docs.wso2.com/display/AM210/apidocs/store/index.html).

For create a new application a user will need **to obtain first an Authorization token Bearer** the first thing than our user    should has is **Internal/subscriber** role, it used to  be by default.
This will be our workflow:
1. Client Registration for get the proper pair ***client-id:client secret*** .
2. Token generation for get the token bearer.
3. Generate the application with the token generated in  the previous step.

We need the steps (1-2) for every process that require **Authorization: Bearer** as is the case of creation of new applications


Remenber that for basic authorization whe need encode64 our Authorization parameter at the Header by the way remember that in Authorization: Basic <encode64(userid:password)> and **userid is case sensitive** see Basic and [Digest Access Authentication specefications](https://tools.ietf.org/html/rfc2617#page-5)

[You can find a reference to process 1-2](https://docs.wso2.com/display/AM210/apidocs/store/index.html#guide)




