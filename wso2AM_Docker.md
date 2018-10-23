
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

It means that when we make a request to an specific endpoint, WSO2 will addresses to the to **the Production URL** (http://172.17.0.4:9000/apirest) + the path to our service (/football/matchs). So finally we are talking about context+path that you can find in your restfull definition.(It is independently of your restfull implementation).

If you try to test the aforementioned **Production URL** or **Sandbox URL** most of the time will fail DO NOT feel that someting is wrong and keep goit. In my opinion I think that the Idea of this validation is wrong and most of de developer spent some time trying to understand what did the make wrong and it was nothing.


## Clustering ##

In the process of clustering api manager, some important info:

1. [Information related with clustering](https://docs.wso2.com/display/CLUSTER44x/Overview): Curiously the information about the last releases make references to earlier relase. The info is no very clear when they try to separate the 4 components() and [how configure it](https://docs.wso2.com/display/CLUSTER420/Clustering+API+Manager) and prone to errors.
2. H2 database that come with WSO2 is [NOT recommended in production environment](https://docs.wso2.com/display/CLUSTER44x/Setting+up+the+Database). 
3. In what escenarios is recommended clustering WSO2 product. What does it mean in the following image in your [clustering documentation page](https://docs.wso2.com/display/CLUSTER44x/Clustering+the+Gateway):
   ![Load balancer api gateway](NGINXBalancer.png)

What is balancing NGINX in that case, because the element are diferent (manager/worker)

Some queries:

1. what files should be saved, WSO2 have a backup implementation?
2. Is not clear if we need to use ENV var in our WSO2 AM, for example when we need to configure our Production URL and our URL is dynamic.
3. Is possible change the error levels? In docker the container write all levels (warn,info,error) perhaps only ERROR or WARN or any other combinations.
4. If not possible the use of dns in our address because the user of Hazelcast what happend with all of our dynamic address that we need to use? We need to start our containers every time that other referenced address change.
5. So is not clear in what scenarios is recommended clustering WSO2 product even the images indicating 

## Unknown procedures while dockerizing ##

Some of the most important aspect that are no clear when deploy WSO2 in docker container:
1. How can I modify configuration elements when I run a container from an specficic image ([WSO2 official site](https://hub.docker.com/u/wso2/)). For example how:

   - Change configuration when running docker image?. We create docker container with volumes BUT 
     in producction environment we need several changes like **H2 DB<=> Postgree/Msql/etc**. Configuring cache and change:
     <PRODUCT_HOME>/repository/conf/carbon.xml, <API-M_HOME>/repository/conf/api-manager.xml, etc.
     
   - 

