---
title: Uplift Basics
layout: default
parent: Uplift Model
nav_order: 5
---

# Uplift Basics
The core idea behind uplift modeling is modeling conditional average treatment effect (CATE) 
which could be formulated below

$$ CATE(x) = \mathbb{E}[Y(1) - Y(0)|X=x]$$

where
- Y(1) is the outcome if the individual receives the treatment
- Y(0) is the outcome if the individual **not** receives the treatment
- X = x denotes the covariates of the individual

If we could have a random collection trial setting (RCT), we could formulate CATE as the below

$$CATE(x) = \mathbb{E}[Y|T=1, X=x] - \mathbb{E}[Y|T=0, X=x]$$





# Appendix
$$\sqrt{3x-1}+(1+x)^2$$

**The Cauchy-Schwarz Inequality**

```math
\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
```

$$
\begin{aligned}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{aligned}
$$