---
title: What's this?
parent: ML Service
layout: default
nav_order: 20
---
# What's this
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

## What's this about?
It's a project building a machine learning service from scratch. From the model training to its deployment.
From building backend REST API to frontend interface. It's plug and play. You could just replace the model while
leave the ml service untouched to run different ML services.

This project is suitable for people who want to have a quick ML service POC for the models they worked on. Enjoy :wine_glass:

## A quick demo
Hit the endpoint `allyoushawn.hopto.org:8080/ml_service` through a browser, we could start using the ML service.

![ml_service_home_page](/docs/ml_service/images/ml_service_home_page.png)

In the page, we see the following elements:
* Id: The task id specified by the user.
* Message: The input of the ML service. Generally it's a sentence.
* A service selection menu: Currently we could choose `sentimentAnalysis` and `machineTranslation`.

After we click `Submit`, the service would give users the corresponding results. In this example, the sentiment score
for the sentence `This is very good.` is `3.0`. (which is ranging from `-5.0` to `5.0`. ) We will talk more about it in 
sentiment analysis section.

![ml_service_sa_result](/docs/ml_service/images/ml_service_sa_result.png)


Let's try the other service, `machineTranslation`. We could see the translated results in Chinese after we submit our
query to the service.

![ml_service_click_menu](/docs/ml_service/images/ml_service_click_menu.png)


![ml_service_mt_result](/docs/ml_service/images/ml_service_mt_result.png)


However, just a disclaimer, you would find weird results when you input different sentences since the service is only
a POC for the serving pipeline. We could spend tons of time tuning the ML models if needed. :stuck_out_tongue: