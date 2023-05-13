---
title: ML Service
parent: ML Service
layout: default
nav_order: 50
---
# ML Service
Refer to the repo READMD for more information.  [Link](https://github.com/allyoushawn/mlservice)

The service serves as an api gateway for ML model services like sentiment analysis and machine translation, etc.
We implement a REST API gateway with `Java` and `Spring` framework. The gateway would take the query and redirect 
the query to the corresponding ML model service to get the corresponding response.

The gateway and the ML model services are all deployed through Docker, and therefore we have to set up the networks for
these containers' communication. 

To communicate with other containers, we have to put these containers into a user-defined bridge network.
We will use a user-defined bridge network named <em>allyoushawn-net</em> as an example.
Check out the [tutorial](https://www.tutorialworks.com/container-networking/) for more information.

Create the bridge network with the following
```
docker network create allyoushawn-net
```

Build image with Docker
```
docker build -t mlservice:base --target base -f deployment/Dockerfile .
```
Run with Docker, while using <em>--net</em> argument to put the container into the network.
```
docker run --name mlservice_local -it -p 8081:8081 --net=allyoushawn-net mlservice:base
```

Similarly, we have to make sure other containers we need to communicate with are put into the network, like
```
docker run --name sentiment_analysis_model_service_local -it -p 4460:4460 --net=allyoushawn-net sentiment_analysis_model_service:prod
```

We also have to make sure we are using the correct hostname in our code for communication.
For example, in [MLServiceController.java](https://github.com/allyoushawn/mlservice/blob/main/src/main/java/com/allyoushawn/mlservice/MLServiceController.java), the SENTIMENT_ANALYSIS_POST_URL has to be the something like <em>sentiment_analysis_model_service_local:4460/sentiment_analysis</em>.  `sentiment_analysis_model_service_local:4460` represents the target container's name and port. 

The following segment in the code enables us to dynamically set up the endpoint through <em>application.properties</em>. The hostname used for docker should be specified in <em>application-docker.properties</em>.
```
@Value("${sentiment_analysis_post_url}")
private String SENTIMENT_ANALYSIS_POST_URL;
```

Finally, to stop and remove the container.
```
docker container stop mlservice_local && docker container rm mlservice_local
```