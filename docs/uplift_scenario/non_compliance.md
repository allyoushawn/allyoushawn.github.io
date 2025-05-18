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

In this approach, we filter the dataset and select the users really receive the intended treatments. However, this selection would break the randomness. If there is confounded factors, the users we select would be systematically different from those we don't, and thus we would introduce bias into the modeling. In general it would not be a good idea.

**Compiler average causal effect (CACE)**

Without losing any data, we estimate the treatment effect among compilers — those who:
- Would take the treatment if assigned to treatment
- Not take the treatment if assigned to control

We will introduce CACE in the below sections.

# CACE

TBA.