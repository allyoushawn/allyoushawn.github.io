---
title: Mediation modeling
layout: default
parent: Uplift model scenarios
nav_order: 5
---
Reference: [Mediation Modeling at Uber: Understanding Why Product Changes Work (and Don’t Work)](https://www.uber.com/blog/mediation-modeling/?uclick_id=ab87d21b-5786-4b35-984f-eef020820c8d)

# Scenario formulation
We start with the most straight ideal case for the uplift modeling. Suppose we have a dataset satisfy the following properties:


1. The dataset is not confounded (e.g. RCT setup)
2. All users receive the treatment effect
3. The treatment effect has the same effects on the users

With the properties, we could use average treatment effects (ATE) to represent the effects brought by the treatment. The below is an example setup:

- Scenario: Uber drivers might file supporting tickets to ask for explanation of their earnings. We want to reduce the number of supporting tickets by showing earning graphs to drivers. 
- Treatment: Showing earning graphs to drivers
- Outcome $$Y$$: The number of filed supporting tickets


# Mediation modeling formulation
However, sometimes we want to know how important a mediator is for the treatment effects. For example, the mediator in this case could be the understanding of the graphs. We want to know if the ATE is caused by the fact that drivers understanding the graph or simply by seeing there is an earning graph without understanding it would have the same treatment effects. So the mediator is

- Mediator $$M$$: Understanding of earning graphs

With the above setup, we model that ATE could be decomposed into two elements: ATE = ADE (average direct effect) + ACME (average causal mediated effect )

- ATE: The total effect
  - Which usually we model as $$\mathbb{E}[Y(1, M(1)) - Y(0, M(0))]$$ where $$M(1)$$ means the mediator is turned on or exists. $$Y(T, M(m))$$ indicates whether the treatment $$T$$ is applied and whether the mediator exists.
- ADE: ADE is the impact from the treatment on the outcome that does not go through the mediator. 
  - Which usually we would model it as $$\mathbb{E}[Y(1, M(0)) - Y(0, M(0))]$$, $$M(0)$$ means the moderator is turned off or not exists.
- ACME: ACME corresponds to the difference in potential outcomes that would occur if we were to flip the mediator into the value it would take under the treatment status while holding the treatment status itself fixed.
  - Which usually we would model it as $$\mathbb{E}[Y(1, M(1)) - M(1, M(0))]$$

![mediation_modeling_diagram](/docs/uplift_scenario/images/mediation_modeling/mediation_modeling_diagram.png)