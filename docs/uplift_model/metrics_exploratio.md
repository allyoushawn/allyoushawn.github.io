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
uplift_score = -| (user_number % converted_parameter) + (random.random() - 0.5) * noise |
```

![uplift_model_data_uplift_score_assignment](/docs/uplift_model/images/metrics_exploration/uplift_score_assignment.png)

Finally, to evaluate our models, we would run some metrics like AUC, blablabla@k.
![uplift_model_metrics_first_glance](/docs/uplift_model/images/metrics_exploration/evaluation_metrics_first_glance.png)

In the following sections, we would introduce each metric and how they are computed.

# Uplift at K
The users (in both control and treatment) would be sorted based on the assigned uplift scores. If `K = 0.01`, it would
mean we compare the top 1% of users in treatment and control and compute the uplift. We get uplift at K with the
following equation:

![uplift_model_metrics_first_glance](/docs/uplift_model/images/metrics_exploration/uplift_at_k_equation.png)

The notation in the above equation is following the
[link.](https://pylift.readthedocs.io/en/latest/introduction.html#the-qini-curve)
`n_{t, y=1}` means the number of users who are converted in the top 1% treatment cohort and `n_t` is the
number of users in the top 1% treatment cohort. 
However, how to select the users
could be tricky. It could be top 1% users from treatment and control respectively. Or, it could be top 1% of users from
the all users. If we select top 1% users from treatment and control respectively, `n_t` and `n_c` should be the same if 
the number of the numbers of all users in treatment and control are similar, which is `N_t = N_c`. On the other hand,
this might not be true if the top 1% of users are selected from all users. 

By tracing the [source code](https://github.com/maks-sh/scikit-uplift/blob/master/sklift/metrics/metrics.py#L474)
of the scikit-uplift computing the metric, we could see the package provide both of them. If strategy is `overall`, the
metric is computed with top 1% of users from the all users.

In the notebook, we use the `overall` strategy and the numbers are as follows and therefore the uplift@0.01 is 0.8.
```
n_{t, y=1} = 10
n_t = 10
n_{c, y = 1} = 2
n_c = 10
```
