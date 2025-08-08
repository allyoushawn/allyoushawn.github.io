---
title: Vision Language Models Basic
layout: default
parent: ML Misc.
nav_order: 40
---

The article is based on the following source:
- [Vision Language Models Explained](https://huggingface.co/blog/vlms)
- [nanoVLM: The simplest repository to train your VLM in pure PyTorch](https://huggingface.co/blog/nanovlm)

We will focus on the LLaVA variant in this article. 

# Vision language models
The term vision language models here we are referring to the LLMs with vision capability. For LLaVA variant VLM, it consists of a pretrained vision module and a pretrained LLM and combined the two with the projector and module called multimodal projector and some fine-tuning. The following figure clearly demonstrates the relations between the components.

![vlm_overview](/docs/ml_misc/vlm_basic/images/vlm_overview.png)

## Training process in high level
LLaVA introduces a module **multimodal projector** to project the vision input to the embedding space of LLM tokens. 

1. Multimodal projector training. Use GPT-4 to generate questions whose answer is the caption. Use the QA set to train the multimodal projector while freezing other modules
2. Instruction fine-tuning. Unfreeze the text decoder and fine tune the model with instruction and the corresponding answers
3. The image encoder is frozen during the whole process

# Image encoder

In this section we would introduce the image encoder used in LLaVA. From the [LLaVA 1.5 paper](https://arxiv.org/pdf/2310.03744) it's suggesting that it's using the [openai/clip-vit-large-patch14-336](https://huggingface.co/openai/clip-vit-large-patch14-336).

# nanoVLM

Our Colab notebook [here](https://github.com/allyoushawn/jupyter_notebook_projects/blob/main/ml_misc/workable_nanoVLM.ipynb).

We use [nanoVLM](https://github.com/huggingface/nanoVLM) for understanding the details of training a VLM. We tweaked the Colab notebook shared by the author to make it runnable with the implementation code when we were studying it.