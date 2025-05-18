---
title: Heterogeneous treatment estimation
layout: default
parent: Uplift model scenarios
nav_order: 10
---

Reference: [Analyzing Experiment Outcomes: Beyond Average Treatment Effects](https://www.uber.com/blog/analyzing-experiment-outcomes/?uclick_id=ab87d21b-5786-4b35-984f-eef020820c8d)


# Scenario formulation
Now let's discuss a more general case:

1. The dataset is not confounded (e.g. RCT setup)
2. All users receive the treatment effect
3. The treatment effect **NOT** has the same effects on the users

# CATE

The most straight forward modeling/analysis we could do is the uplift modeling which is aiming for conditional Average Treatment Effect (CATE). The uplift modeling allow us to understand the personalized treatment effects. It has been discussed a lot in the [uplift model section](https://allyoushawn.github.io/docs/uplift_model/).

# Quantile regression (QTE)

Reference: [Analyzing Experiment Outcomes: Beyond Average Treatment Effects](https://www.uber.com/blog/analyzing-experiment-outcomes/?uclick_id=ab87d21b-5786-4b35-984f-eef020820c8d)

The other analysis approach is quantile regression (QTE).

Sometimes the ATE seems 0 while different quantile has different response to the treatment. Quantile regression estimates the impact of a treatment across different points (quantiles) of the outcome distribution, rather than focusing solely on the mean.


# Example
Imagine Uber is testing a new driver assignment algorithm to reduce rider wait times. We run an A/B test with the following setup:
- Control group gets the old algorithm
- Treatment group gets the new one

When analyze different percentile of waiting time in control and treatment groups, we have the following table:

| Quantile    | Control Wait Time (min) | Treatment Wait Time (min) |
| -------- | ------- | ---- |
| 10%  | 2    | 2    |
| 50% | 6     |  4  |
| 90%    | 12    |  8  |

When we do the quantile regression analysis:

| Quantile    | QTE (Treatment − Control) |
| -------- | ------- | ---- |
| 10%  | 2  - 2 = 0   |
| 50% | 4 - 6 = -2  |
| 90% |  8 - 12 = -4  |


If we looked only at the Average Treatment Effect (ATE), and obtained ATE = −1.6 minutes from the below numbers:
- Mean in control = 6.8 minutes
- Mean in treatment = 5.2 minutes 



On the other hand QTE could help us understand that:
- Slowest users benefit the most.
- Fastest users see no change.

The above are the insights that QTE could bring us.