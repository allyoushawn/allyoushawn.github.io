---
title: AliCCP dataset
parent: Dataset
grand_parent: RecSys
layout: default
nav_order: 1
---
# Multitask-learning in recommendation system
In the Recommendation system domain, especially for ranking, it is very common to train a multi-task learning model (MTL) to learn different objectives at once so that the model could learn:
1. Balance different business need and objective: E.g. balancing the CTR target vs the watching/reading time target. (Click-bait items vs meaningful content)
2. Extract useful features from different label perspectives: E.g. insights for the high CTR but low watching/reading time vs high CTR and high watching/reading time

Therefore, we need a dataset that contains multiple labels to enable us evaluating different MTL algorithms. Further, an ideal dataset should be constructed from the real world user logs so that the evaluation is based on the real world distribution instead of a synthesized/hypothesized distribution.

# Ali-CCP dataset

Fortunately, [Alibaba](https://www.alibaba.com) has published such dataset: **Alibaba Click and Conversion Prediction (Ali-CCP, [link](https://tianchi.aliyun.com/dataset/408) )**  It was introduced in the well-known [ESMM paper](https://arxiv.org/pdf/1804.07931). This dataset is built from the real world traffic logs in Taobao and it is a loarge scale dataset. (~42M for train and eval respectively)

The data source illustration is as the below screenshot (shared from the Ali-CCP website  [link](https://tianchi.aliyun.com/dataset/408))
![Ali-CCP data source illustration](/docs/recsys/dataset/images/aliccp_dataset/aliccp_taoboa_pic.png)

The below is the provided files for downloading and their unzipped file size (shared from the Ali-CCP website  [link](https://tianchi.aliyun.com/dataset/408)) It separates out the features into one file and per-example labels into another file to reduce the storage cost
![Ali-CCP data structure overview](/docs/recsys/dataset/images/aliccp_dataset/aliccp_data_structure_high_level.png)


## Data samples

Conceptually, each sample is composed of the items shown in the following (shared from the Ali-CCP website  [link](https://tianchi.aliyun.com/dataset/408)) :
![Ali-CCP sample skeleton](/docs/recsys/dataset/images/aliccp_dataset/aliccp_sample_skeleton.png)

* Has two kins of label: click and conversion
	* Conversion = 1 means click must = 1
*
