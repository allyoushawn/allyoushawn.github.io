---
title: Handling noncompliance
layout: default
parent: Uplift model scenarios
nav_order: 15
---

# Scenario formulation
Now let's discuss a more general case:

1. The dataset is not confounded (e.g. RCT setup)
2. **NOT** all users receive the intended treatment effect

In this scenario, the following could happen

- Treatment group users don’t comply (i.e. don’t receive the treatment)
- Control group users cross over (i.e. receive the treatment)

# Solution overview

**Intention-to-treat (ITT)**

With this approach, we model the intention instead of whether the users really receive the treatment. Therefore, we do not add additional assumptions and preserve the randomness of the dataset. However, the limitation of this approach is that the noncompliance would dilute the treatment effects.


**Per protocol/As-treated**

In this approach, we filter the dataset and select the users really receive the intended treatments. However, this selection would break the randomness. If there is confounded factors, the users we select would be systematically different from those we don't, and thus we would introduce bias into the modeling. In general, it would not be a good idea.

**Complier average causal effect (CACE)**

Without losing any data, we estimate the treatment effect among compilers — those who:
- Would take the treatment if assigned to treatment
- Not take the treatment if assigned to control

We will introduce CACE in the below sections.

# CACE

Let's start with the equation, and we could dive deeper later.

$$
\textrm{CACE} = \frac{\textrm{ITT}}{\textrm{Compliance rate}} = \frac{\mathbb{E}[Y|T=1] - \mathbb{E}[Y|T=0]}{\mathbb{E}[D|T=1] - \mathbb{E}[D|T=0]}
$$

In the above equation, $$D$$ means the expectation of actual receive treatment variable. Therefore, the equation could be viewed as making ITT corrected by a compliance rate term.  

An example is as the below:

- We have 100 people in our dataset. 50 in treatment group, 50 in the control group.
- Only 30 users in the treatment actually take the treatment, and all 50 users in the control not take the treatment
    - All control group users are compliers and only 60% of users in the treatment are compliers
- The average outcome of the treatment group is 60 and 50 for the control group
- Based on the above we have the following
    - ITT: 60 - 50 = 10
    - Compliance rate: 0.6 - 0 = 0.6
    - CACE: 10 / 0.6 = 16.67

## Complier
We need to know that in reality there is no way we could understand who are compliers without assumptions. The reason is that the complier's concept is based on counterfactual observation: Users would take the treatment if in the treatment group and would not take the treatment if in the control group. However, we could not assign a users in treatment group and control group simultaneously. Therefore, we could only use group estimate as the above to estimate the compliance rate.