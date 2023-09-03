---
title: Uplift Model Metrics
layout: default
parent: Uplift Model
nav_order: 10
---
Before we jump into how to train uplift models, let's start with understanding the metrics used by these models.

[Jupyter Notebook](https://github.com/allyoushawn/algorithms/blob/master/uplift_model/uplift_metric_exploration.ipynb)

In general, the data for training/testing uplift models will look like this:
We have a control group and treatment group. In this case the two groups contain same number of users.

![uplift_model_data_user_group_creation](/docs/uplift_model/images/metrics_exploration/user_group_creation.png)

For the two groups, we assume that users in the treatment group have been given treatment like showing some ads while
the users in the control group have not. For each user we would assign a label. For example, suppose we show treatment
users some ads, and we want them to buy more. The label here is whether the user is converted (i.e. buy something.) 

In the notebook, we assign the converted label based on the user number. If the user is in the treatment group,
users having `user_number % converted_param = 0` would be assigned converted label. Here `converted_param` is a 
parameter used to control how many users are converted. 

If the user is in the control group,
we would apply an additional randomization to control how many control users are converted. In the notebook, we could
see that the conversion rate for the treatment group is ~10% and ~5% for the control group.

![uplift_model_data_label_assignment](/docs/uplift_model/images/metrics_exploration/label_assignment.png)

Next, we have an uplift model to predict the uplift scores for our users. Here the score is assigned based with
the following equation where `noise` is a scalar controlling the model performance. This assignment seems pretty close
to the ground truth.
```
score = -| (user_number % converted_parameter) + (random.random() - 0.5) * noise |
```

![uplift_model_data_uplift_score_assignment](/docs/uplift_model/images/metrics_exploration/uplift_score_assignment.png)