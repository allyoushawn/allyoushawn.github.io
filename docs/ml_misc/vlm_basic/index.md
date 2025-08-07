---
title: Vision Language Models Basic
layout: default
parent: ML Misc.
nav_order: 40
---

The article is based on the following source:
- [Vision Language Models Explained](https://huggingface.co/blog/vlms)

We will focus on the LLaVA variant in this article. 

# Vision language models
The term vision language models here we are referring to the LLMs with vision capability. For LLaVA variant VLM, it consists of a pretrained vision module and a pretrained LLM and combined the two with the projector and module called multimodal projector and some fine-tuning. The following figure clearly demonstrates the relations between the components.

![vlm_overview](/docs/ml_misc/vlm_basic/images/vlm_overview.png)
