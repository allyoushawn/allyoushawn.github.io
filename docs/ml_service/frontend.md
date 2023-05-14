---
title: Frontend
parent: ML Service
layout: default
nav_order: 60
---

# Frontend 
Refer to the repo README for more information.  [Link](https://github.com/allyoushawn/https://github.com/allyoushawn/mlservicefrontend)

To interact with our ML service we could either do it with command line interface or with a more friendly way: browsers.
We build a naive interface like the following:

![ml_service_home_page](/docs/ml_service/images/ml_service_home_page.png)

In the interface, users would enter an id associated with their query and a message that needs to be processed by our
ML models. Lastly we provide a menu for users to choose which ML model service they would like to have. Currently, they
could choose either `sentimentAnalysis` or `machineTranslation`. The interface would convert the input information to a 
POST request and query our ML gateway service to get the corresponding response.

# Next
We are going to use tools to test the throughput of our service.