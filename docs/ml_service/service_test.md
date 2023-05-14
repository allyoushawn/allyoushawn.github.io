---
title: Service Testing
parent: ML Service
layout: default
nav_order: 70
---
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

# Testing with JMeter
To know the performance of our service, we could use `JMeter` to set up
the tests we want and see if we need to adjust the setup of our service or improve our models.
Here is a nice [tutorial](https://www.guru99.com/jmeter-performance-testing.html) 
to illustrate how to use JMeter to set up the testing.

We set up 100 users to query our service and each user would query our service 10 times.
The following are the test results. 

![ml_service_sa_test](/docs/ml_service/images/ml_service_sa_result.png)

![ml_service_mt_test](/docs/ml_service/images/ml_service_mt_result.png)
