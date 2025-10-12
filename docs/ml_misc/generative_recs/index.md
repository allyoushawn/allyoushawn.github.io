---
title: Generative Recommendation Systems
layout: default
parent: ML Misc.
nav_order: 50
---

This article is based on the following content
- Paper [Recommender Systems with Generative Retrieval (TIGER)](https://arxiv.org/pdf/2305.05065)
- Tech blog [Training an LLM-RecSys Hybrid for Steerable Recs with Semantic IDs](https://eugeneyan.com/writing/semantic-ids/)


# Background

Current recommendation system is based on the two staged system. The first phase is candidate generation which has multiple channels covering different aspects of the system and each channel retrieves the candidate items for the next stage. The second phase is ranking phase. A large ranking model would rank the items from the first phase and decide the final ranking. This model would need to balance different objectives of the recommendation system and therefore it is very often that it is built in a multi-task learning setup.

For the first phase retrieval, it is usually done by embedding query search. That is, items are represented as embeddings. During the retrieval we would prepare the query embedding containing the relevant information and use nearest neighbor search to search for the top K items for the second phase.

Recently there is a trend that the retrieval is using autoregressive-style generate the identifiers for the retrieved items. The retrieval becomes decoding the semantic id tokens through a LM-like process instead of a nearest neighbor search. 

Benefits:
- Semantic id decoding could have better cold-start and long-tail generalization
- The LM integration unlocks the power of user prompting and provide steerable RecSys experience


# Semantic ID

The concept of semantic ID is proposed by Google's [TIGER paper](https://arxiv.org/pdf/2305.05065). An overview could be illustrated with the below Figure from the paper.


![semantic_id_decoding](/docs/ml_misc/generative_recs/images/semantic_id_decoding.png)

From the above figure we could see that each item is mapped to a code composed with three integers named semantic ids. These semantic ids they contain the relations between the items and therefore they could better be used in the LM-like training and application. In other wrods, the semantic ids are designed to have the following properties:
- Similarity: The similar items should have similar semantic ids
- Hierarchy. For an item with semantic id (10, 21, 35), item A (10, 23, 37) and item B (15, 21, 35), the item is more similar to item A since they have the same code on the first layer

## RQ-VAE

**My implementation**
- [source code](https://github.com/allyoushawn/recsys_playground/tree/20250908_tiger_dev/tiger_semantic_id_amazon_beauty)
- [execution notebook results](https://github.com/allyoushawn/jupyter_notebook_projects/blob/main/ml_misc/tiger_semantic_id_amazon_beauty.ipynb)



In the TIGER paper, the authors proposed using Residual-Quantized Variational AutoEncoder (RQ-VAE) to train the model.

![rq_vae](/docs/ml_misc/generative_recs/images/rq_vae.png)
