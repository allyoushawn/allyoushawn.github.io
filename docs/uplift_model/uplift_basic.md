---
title: Uplift Basics
layout: default
parent: Uplift Model
nav_order: 5
---

# Uplift Basics
The core idea behind uplift modeling is modeling conditional average treatment effect (CATE) 
which could be formulated below

$$ \textrm{CATE}(x) = \mathbb{E}[Y(1) - Y(0)|X=x]$$

where
- $$Y(1)$$ is the outcome if the individual receives the treatment
- $$Y(0)$$ is the outcome if the individual **not** receives the treatment
- $$X = x$$ denotes the covariates of the individual
- We assume it is a binary treatment setting

However, in the real world we could never observe $$Y(1) - Y(0)$$ for an individual because
a user could never be treated and not-treated at the same time, and it is the fundamental challenge of causal inference.

In real world, the dataset we could obtain is 
observational data: $$\mathbb{E}[Y|T=1, X=x]$$ and $$\mathbb{E}[Y|T=0, X=x]$$
and they are not necessarily the same as $$Y(1)$$ and $$Y(0)$$.

## Confounding bias
Let's take a step back and see why $$\mathbb{E}[Y(1) - Y(0)|X=x] \neq \mathbb{E}[Y|T=1, X=x] - \mathbb{E}[Y|T=0, X=x]$$.

Suppose we want to know whether seeing an online ad increases the likelihood of a user making a purchase. 
We’re interested in the effect of ad exposure (treatment) on purchase behavior (outcome) 
for a specific group of users with characteristics $$X = x$$ The goal is we want to estimate $$\mathbb{E}[Y|T=1, X=x]$$, 
which is the expected likelihood of purchase if everyone in this group saw the ad. 
Also, the dataset is not collected randomly. 

Under this setting, people who see the ad are often systematically different from those who don’t, 
creating **confounding**. For example, people seeing the ad might intrinsically have higher tendency to purchase.
The $$\mathbb{E}[Y|T=1, X=x]$$ obtained through the dataset will have **confounding bias** 
since it's being inflated by the mentioned phenomenon 
when we compare it to the true value we want $$\mathbb{E}[Y|T=1, X=x]$$.


## Random collection trial (RCT)
From the above section, we could see that the reason behind the confounding bias is that the covariates $$x$$ is not
general enough. If we could have general enough $$x$$ to cover all aspects, the confounding bias would be removed.

In fact, the first, intuitive approach to dealing with confounding bias is random collection trial. in this set up, the
$$x$$ in our dataset is collected randomly and therefore would be general enough to remove confounding bias.

Mathematically, it is called **conditional independence assumption** or **ignorability**. 

$$ Y(0), Y(1) \perp\!\!\!\perp T | X $$

Under this setting, we would have

$$\mathbb{E}[Y(1)|X=x] = \mathbb{E}[Y|T=1, X=x]$$

However, what should we do if we could not perform random collection trial?

Under this setting, people who see the ad are often systematically different from those who don’t, 
creating **confounding**. For example, people seeing the ad might intrinsically have higher tendency to purchase.
The $$\mathbb{E}[Y|T=1, X=x]$$ obtained through the dataset will have **confounding bias** 
since it's being inflated by the mentioned phenomenon 
when we compare it to the true value we want $$\mathbb{E}[Y|T=1, X=x]$$.

Test again $$\mathbb{E}[Y|T=1, X=x]$$.

Test again 2 $$\mathbb{E}[Y(1)|X=x] = \mathbb{E}[Y|T=1, X=x]$$.



