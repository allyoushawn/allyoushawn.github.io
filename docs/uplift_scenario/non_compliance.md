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
We need to know that in reality there is no way we could understand who are compliers without assumptions. The reason is that the complier's concept is based on counterfactual observation: Users would take the treatment if in the treatment group AND would not take the treatment if in the control group. However, we could not assign a users in treatment group and control group simultaneously. Therefore, we could only use group estimate as the above to estimate the compliance rate.

# CATE for Non-compliance

(More on ignorability [here](https://allyoushawn.github.io/docs/uplift_model/uplift_basic.html#random-collection-trial-rct))

CATE models the outcome given the treatment assignment and individual features $$X$$. It requires the ignorability assumption.

Let's recap the ignorability assumption. The ignorability assumption is when we condition on $$X$$, the only difference of $$Y(0)$$ and $$Y(1)$$ comes solely from the different treatment.

$$ Y(0), Y(1) \perp\!\!\!\perp D | X $$

- Note: Usually we use $$T$$ in the equation. However, in this article $$T$$ is used for the treatment assignment and $$D$$ is for the actual treatment received. In most cases they should be the same while when we are discussing non-compliance they would not, so we use $$D$$ here.

However, the existence of the non-compliance could break the assumption since $$D$$ would be systematically different from random. If some factors unobserved in $$X$$ drive the non-compliance, the assumption will no longer hold, and we will need to handle it. Below are two example approaches

## Instrumental variable CATE (IV-CATE)

Instrumental variable (IV):
- Usually, is represented with notation $$Z$$, but here is $$T$$ and will be illustrated below 
- Is a variable that allow us to estimate causal effects when the ignorability fails particularly due to the non-compliance
- For the context here, it is the treatment assignment. In comparison to IV, $$D$$ here represents really receive the treatment effects
- Assumption
    - IV affects $$D$$
    - IV has no direct impacts on the outcome $$Y$$. It only influences $$Y$$ through $$T$$

We also need the assumption that IV satisfies the ignorability. $$Y(0), Y(1) \perp\!\!\!\perp T|X$$

From the above properties of IV, we could see that IV-CATE is based on the CACE concept and IV here is for estimating the Intent-to-Treat causal effects. The IV-CATE is calculated as below

$$
\textrm{IV-CATE} = \frac{\mathbb{E}[Y|T=1, X=x] - \mathbb{E}[Y|T=0, X=x]}{\mathbb{E}[D|T=1, X=x] - \mathbb{E}[D|T=0, X=x]}
$$

To build the model, we need the dataset with $$Y, X, T, D $$.

## Propensity adjustment

We use $$X$$ to model selection into treatment, and then recover CATE. In IV-CATE, we need two labels regarding the treatment: $$T$$ and $$D$$ and train a model $$P(D|Z=z, X=x)$$ to estimate the compliance. 

However, in the real world application where observational data is more available which does not have $$T$$ since the treatment assignment concept is not included in the data, we would need to ditch $$T$$ in our modeling. On the propensity adjustment track, we directly model $$P(D|X=x)$$

Note that the price of ditching the instrument variable $$T$$ which is an easier variable to guarantee ignorability is that we need the ignorability assumption on $$D$$ by providing a rich enough $$X$$ to make sure we do not have unobserved factors that would break the ignorability assumption. 

Example approaches here are DR Learners, Dragon Net. (Introduced [here](https://allyoushawn.github.io/docs/uplift_model/dragonnet.html).)