---
title: Treatment predictive features
layout: default
parent: Uplift model scenarios
nav_order: 15
---

# An imbalanced RCT dataset
Imagine the below setup:
- We want to conduct a RCT experiment for uplift modeling and the treatment $$T$$ is awarding students with scholarships
  - The student in the treatment group would be awarded with scholarships  
- Y is students' future job salary 
- The experiment is totally random, while for some reason we found that students in the treatment group has slightly higher GPA in general. In other words, using GPA as a feature would tip us which group the users is in. 


Two common questions would be raised regarding this dataset
1. If we still treat the dataset as the dataset collected from RCT, will the trained model be biased? 
2. Should we still include the GPA as the feature while it would sort of tell us which group the student is

For the first question, the model would not be biased due to the GPA imbalance IF we assume the ignorability assumption holds which is a valid assumption with the RCT setup. The randomness ensures there is no confounding protects our causal estimation.

For the second question, the answer is yes, we should include the GPA feature for better outcome prediction and preventing missing any confounding factors. By conditioning on GPA, the model is able to compare the treatment effects among users with same GPA.

## Dropout students
Now let's add more constraints. Suppose that if a student has lower GPA, he would have higher chance to drop the school and being removed from the dataset, is the dataset still valid?

In this case, the dataset is no longer fully valid. The reason is that the missing is not fully random.

# Treatment predictive features
Imagine a scenario that we trained a causal model with a dataset and the model's performance is good. However, when we do the t-Test on the features, we find some features are imbalanced among different treatment groups. That is, when we compare feature $$x$$ distribution between the treatment and control group, we see the p-value is lower than a threshold say 0.05. 

We are tempted to think that:

1. The feature causes the data leakage through signals of the treatment groups
2. The signals are picked up by the model
3. The model has a deceptive good performance
4. Therefore, we should scan through the features and remove the features that leak the signals

## Why it's possible to see the imbalance

1. The RCT setup ensures independence, not equal distribution. The setup only ensures the probabilistic balance, and it's possible that the finite samples are unbalanced. (For flipping a fair coin 100 times, and we might get 53 heads and 47 tails.)
2. When we are scanning through the features and do t-test, we would encounter [multiple testing issues](https://en.wikipedia.org/wiki/Multiple_comparisons_problem). If we have 1000 features and use 0.05 as significance level, we would expect ~50 features to be significantly different even if the assignment is random.
3. Here we check one feature at a time, and it's a marginal balance check up. It's possible that we see marginal imbalance but if we check the joint distribution together with other features we would see the imbalance is gone.

If we don't have domain knowledge or a strong reason, we should not remove these features. As a side note, if they are confounding factors, we would need to condition on them to hold the ignorability assumption.

## What should we do instead

For model training, use more robust approaches. For example, use honesty tree in the causal forest training.
