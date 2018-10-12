## This document is refered to Restful WSO2 api manager ##

Our goals: 
- Make a sign up 
- This new user has to be capable of:
  - add new applications 
  - subcribe to new Apis
  
  Sign up:
  
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
```sh
 
 
 [In this website all content is deprecated with the exception of Sign up rest service.](https://docs.wso2.com/display/AM200/Store+APIs#StoreAPIs-UserSignup)
  
