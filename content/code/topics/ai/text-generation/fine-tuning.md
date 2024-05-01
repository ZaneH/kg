---
title: Fine Tuning Locally
date: 03-31-2024
---

After a few months of dealing with cloud GPUs, I decided to get a used 12GB VRAM GPU for my desktop. Hopefully I'll be able to train at least 1 useful model on it.

## Overview

There are several tools for fine-tuning models. My current favorite is [Axolotl](https://github.com/OpenAccess-AI-Collective/axolotl). It's obviously more complicated than using OpenAI's platform, but it's free and you can customize it to your heart's content. When fine-tuning, having more VRAM is always better. I've found that 12GB is the minimum for training, but 24GB is certainly ideal. Even then, I imagine 24GB will be limiting even still. At this point, I've accepted that for large tasks, I'll need to use cloud GPUs.

## Use PyTorch Docker Images

During the first few tries, I was install pip packages to my local machine. This was a mistake. There are so many versioning issues that can arise. Instead, I recommend using the official PyTorch Docker images with:

```bash
docker run --gpus all --rm -ti --ipc=host pytorch/pytorch:latest
```

and doing all of your work within the container.

## Fine-Tuning with Axolotl

1. Prepare your dataset in a standard format (alpaca, etc.)
2. Specify your base model, model type and tokenizer type
3. Run the fine-tuning command