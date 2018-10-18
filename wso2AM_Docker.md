
## Dockerizing WSO2 Api Manager ##

WSO2 has a place for [WSO2 docker file documentation](https://docs.wso2.com/display/DF120/WSO2+Dockerfiles+Documentation). I've made a review and I do not like at all at least for WSO2AM.

Any way my first recommendation is ALLWAYS USE OFFICIAL IMAGES of course if it possible. I have test to many images from WSO2 
and the best perfomance is [WSO2 official site](https://hub.docker.com/u/wso2/).

The problem: **The documentation is minimal or no documentation.**

**In this kind of product is very important create a container with state, because you will spend too many time in its configuration**  
So before download the image and run it **pay attention in deep** about [how create Volumes](https://docs.docker.com/storage/) in docker:

We will show the basic procedure in which you don't have to worry about where our info  is save:

```sh
# wso2scadip: it is a volume name in docker volume area
# /home/wso2carbon/wso2am-2.6.0/repository: it is the content into the container that we want to store in 
# the docker volume area

sudo docker run --name wso2test -v wso2scadip:/home/wso2carbon/wso2am-2.6.0/repository wso2/wso2am:2.6.0
```
Some ref. from the API creation process:
[Creating API from scratch](https://docs.wso2.com/display/AM260/Quick+Start+Guide#QuickStartGuide-CreatinganAPIfromscratch):
- in step 4 you have to indicate the context 
- in the step 5 you have to indicate teh Production and Sandbox urls

So as I mention befor in one step of our API creation process you have to indicate:

  Production URL: http://172.17.0.4:9000/apirest 
  
  Sandbox URL: http://172.17.0.4:9000/apirest

It means that when we make a request to an specific endpoint, WSO2 will addresses to the to **the Production URL** (http://172.17.0.4:9000/apirest)+ the path to our service (/football/matchs). So finally we are talking about context+path that you can find in your restfull definition.(It is independently of your restfull implementation).

If you try to test the aforementioned **Production URL** or **Sandbox URL** most of the time will fail DO NOT feel that someting is wrong and keep goit. In my opinion I think that the Idea of this validation is wrong and most of de developer spent some time trying to understand what did the make wrong and it was nothing.

Thing that we doubts know:

- what files should be saved, WSO2 have a backup implementation?
- Is not clear if we need to use ENV var in our WSO2 AM, for example when we need to configure our Production URL and our URL is dynamic.



