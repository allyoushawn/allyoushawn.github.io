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

We use [nanoVLM](https://github.com/huggingface/nanoVLM) for understanding the details of training a VLM. We tweaked the [Colab notebook](https://colab.research.google.com/github/huggingface/nanoVLM/blob/main/nanoVLM.ipynb) shared by the author to make it runnable with the implementation code when we were studying it.

When we list the elements in a batch data, we see

- input_ids
- attention_mask
- images
- labels

## input_ids

When we print the content of an input_ids sequence, we see the following structure
```text
<im_end><im_end>...<im_start>user<row1_col1><image><image>...<row1_col2><image>...<image>Question...<im_end><im_start>assistant Answer: A<im_end><im_start>user...
```

- It would start with a sequence of `<im_end>`
- Following `<im_start>user` and a sequence of image related tokens
- After the image sequence token, it would have the question and following an `<im_end>`
- Next, start with `<im_start>assistant` and following the corresponding answer and another `<im_end>`
- The above is one back-and-forth between the user and the assistant. The following `<im_start>` would kick off another back-and-forth between the user and the assistant

![input_ids_example1](/docs/ml_misc/vlm_basic/images/input_ids_example1.png)


**Why there are multiple `<im_end>` at the beginning?**
- `<im_end>` is the padding token in this notebook
- We do the left side padding here
- However, if we do `print(tokenizer.padding_side)` we would see it's right
- The reason is we don't use the tokenizer to do the padding. In the codebase we do the padding ourselves [here](https://github.com/allyoushawn/nanoVLM/blob/main/data/collators.py#L52).