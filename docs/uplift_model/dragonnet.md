---
title: Dragon Net
layout: default
parent: Uplift Model
nav_order: 15
---

# Dragon Net
Dragon net is the model combining the uplift modeling and deep learning. It is proposed in this [paper](https://arxiv.org/pdf/1906.02120). In the paper, it used binary treatment as the example. The model structure is as the below figure. The input `X` is feed into layers of neurons which is the feature extraction process. Once the feature representation `Z` is extracted, there are three heads following. One head is generating the propensity score ($$\hat{e}$$) which is predicting the probability of the input receives treatment. The other two heads ($$\hat{f}_1$$ and $$\hat{f}_0$$) are predicting the outcome of receiving the treatment and not receiving the treatment.

![dragonnet_structure](/docs/uplift_model/images/dragonnet/dragonnet_structure.png)

Intuitively, the loss would be the following

$$\sum_{i} [y_i - \hat{f}_{T_i}(x_i)]^2 + \lambda Xent(T_i, \hat{e}(x_i))$$

However, the $$\hat{f}_{T_i}$$ estimator above would suffer from the confounding bias since the loss does not consider the interaction between the uplift and the propensity score.

## Targeted Regularization

The author used the section 3 to illustrate the idea of targeted regularization. The loss function is the below

$$ T-Loss = \frac{1}{n}\sum_i \{y_i - [\hat{f}_{T_i}(x_i) + \epsilon [\frac{T_i}{\hat{e}(x_i)} - \frac{1-T_i}{1 - \hat{e}(x_i)}]   ]  \}^2$$
