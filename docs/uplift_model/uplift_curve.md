# (Draft) Uplift curve

## Random Performance

[Source code](https://github.com/maks-sh/scikit-uplift/blob/master/sklift/viz/base.py#L186)

From the source code we could see the baseline curve is a straight line. The performance is computed with:

![uplift_model_random_performance_equation](/docs/uplift_model/images/metrics_exploration/Qini_curve_random_performance_equation.png)

The first part of the equation is the overall uplift effects computed by considering all users' conversion behavior.
In the random scenario, we believed that the uplift is fixed given any set of users, and therefore it is a constant.
The overall uplift would be the number of targeted users, `n_c + n_t` times the overall uplift effects.

## Perfect Performance
[Source code](https://github.com/maks-sh/scikit-uplift/blob/master/sklift/metrics/metrics.py#L277)

From the source code, we could see that the perfect performance curve is first computing the perfect uplift score
given the conversion label and the treatment label (indicating users are in the treatment or control group.) The users
are ranked by the perfect uplift scores, and we compute the uplift by targeting different number of users.

Here, the number of targeted users is obtained by considering all users instead of each group. That is, the targeted
users might not contain control or treatment users.

By inspecting the [perfect uplift score computation](https://github.com/maks-sh/scikit-uplift/blob/master/sklift/metrics/metrics.py#L277),
`y_true * treatment - y_true * (1 - treatment)`,
we could see that the users are ranked in the following order:

1. Treatment users with converted label 1
2. Treatment users with converted label 0 or Control users with converted label 0
3. Control users with converted label 1

For each targeted user number, the Qini curve is computed with the following equation:

![uplift_model_qini_uplift_equation](/docs/uplift_model/images/metrics_exploration/Qini_curve_qini_uplift_equation_equation.png)

It is computed with the following [code](https://github.com/maks-sh/scikit-uplift/blob/master/sklift/metrics/metrics.py#L267)
```
curve_values = y_trmnt - y_ctrl * np.divide(num_trmnt, num_ctrl, out=np.zeros_like(num_trmnt), where=num_ctrl != 0)
```

Comparing it with the one used in random performance, we could see that the only difference is the first part now is
not a constant and is dependent of the assigned uplift score.

Let's deep into what happens in each section of the perfect performance curve.
