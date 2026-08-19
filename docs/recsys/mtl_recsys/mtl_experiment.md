---
title: MTL Experiment
layout: default
parent: Multi-task learning for RecSys
grand_parent: RecSys
nav_order: 1
---

Here we conducted the experiments using the popular multi-task learning models and compare their performance.

# Dataset
We used the Ali-CCP dataset for the experiments here. The details of the dataset has been introduced [here](https://allyoushawn.github.io/docs/recsys/dataset/aliccp_dataset.html).

## Dataset processing
The Ali-CCP dataset would be first processed by the processing code [here](https://github.com/allyoushawn/recsys_playground/tree/main/datasets/aliccp) so that we have the artifacts having joined features for each impression and ready to be loaded for training. 

1. [extract.py](https://github.com/allyoushawn/recsys_playground/blob/main/datasets/aliccp/extract.py): Extract the compressed file (.tar.gz) into .csv
2. [data.py](https://github.com/allyoushawn/recsys_playground/blob/main/datasets/aliccp/data.py):


