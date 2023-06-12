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

If we want to test our service, we set up say 100 users to query our service and each user would query our service 10 times.
We would provide more test results in the future when we have specific requirements for the service and show how our 
changes in configs give in different results.
