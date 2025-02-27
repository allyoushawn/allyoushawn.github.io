---
title: TransTEE
layout: default
parent: Uplift Model
nav_order: 20
---

# TransTEE

The [paper](https://arxiv.org/pdf/2202.01336) introduced how to leverage the Transformer structure for the treatment effect estimation (TransTEE). Generally, the transformer's input is a sequence of vectors, and therefore it is not straight forward to apply it to treatment effect estimation scenario which only has one feature vector per user. In the paper, the concept of sequence comes from two places

- Obtain an embedding for each feature (covariate) and therefore an input feature vector for a user with size $$R^{p}$$ could be converted to a matrix $$R^{dxp}$$ where $$d$$ is the embedding dimension.
- For each treatment we also have an embedding. In this case when two treatments are applied to the user and we want to estimate the treatment effects, we would also obtain a sequence of vectors for the treatment


The below figure shows the structure of TransTEE. We concatenate the treatment and the dosage embedding and use MLP obtain the representation. Note here that the dosage input is not required while the paper uses the setup of continuous treatment in the medical field, and therefore it also uses dosage as an optional input. If multiple treatments are applied simultaneously, these treatments would be passed through series of self-attention to get the final representation for the treatments. On the other hand, for the input user features $$x$$, it is passed through the embedding layer and the self-attention modules to capture the interaction between each feature dimension and obtain the final representation of each feature dimension. Finally, these feature representation would be treated as the memory (i.e. key and values for attention) in the Transformer decoder structure and the treatment representation would be treated as the query.

In this way with the Transformer decoder structure we could get the final representations and use an output layer to convert them to a continuous output. Need to note that if we applied multiple treatments simultaneously, we would have more than one representation before the output layer. In the paper it used pooling to merge these representations and do the treatment effects prediction. 

![transtee_structure](/docs/uplift_model/images/transtee/transtee_structure.png)