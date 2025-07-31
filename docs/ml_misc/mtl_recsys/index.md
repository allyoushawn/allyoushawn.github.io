---
title: Multi-task learning for RecSys
layout: default
parent: ML Misc.
nav_order: 30
---

The article is based on the following source:
- [The Evolution of Multi-task Learning Based Video Recommender Systems - Part 1](https://blog.reachsumit.com/posts/2024/06/multi-task-video-recsys-p1/)
- [Mixture-of-Experts based Recommender Systems](https://blog.reachsumit.com/posts/2023/04/moe-for-recsys/)
- [Mixture of Experts Explained](https://blog.reachsumit.com/posts/2023/04/moe-for-recsys/)

# Why multi-task learning (MTL)
Nowadays, an industry-level recommendation system (RecSys) often uses a MLT model for their ranking. 
- **Requirement for multiple objectives**: For example, a video recommendation system would need to balance the click-through-rate (CTR), video watch completion rate, user watch time, user retention...etc.
- **Better model performance**: Among the objectives, Some of them are correlated while some are conflicted. MLT learns relevant information from different objectives and theoretically could give us a model that are more generalized.
- **Better serving efficiency**: For serving different tasks, a MTL model could save a lot of computations since many parameters are shared 

# Shared-bottom MTL
- The simplest structure
- The bottom learned the features that are shared across all tasks and the task specific information is learned in the task towers
- Sensitive to relationships among tasks
  - Weak or complex relations between tasks would lead to performance degradation (negative transfer)
    - The structure design (inductive bias) of shared bottom is conflicted with the fact that the tasks are unrelated or even conflicted
- More on negative transfer
    - MTL results in worse performance on some/all tasks when these tasks are trained individually
        - Knowledge obtained from other tasks is useless/harmful
    - Potential causes
        - Conflicting Gradients
        - Gradient Magnitude Differences
        - Imbalanced Loss Scales
        - Task Conflicts
        - Knowledge Interference
- Seesaw effect issue
    - Improve one task and hurt others

![shared_bottom_mlt](/docs/ml_misc/mtl_recsys/images/shared_bottom_mtl.png)