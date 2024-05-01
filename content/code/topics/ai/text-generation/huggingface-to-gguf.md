---
title: HuggingFace to GGUF
description: How to convert a Hugging Face model to GGUF format
date: 03-31-2024
tags: ai
---

Recently stumbled on an interesting Hugging Face model and saw that the files consisted of `pytorch_model-00001-of-00002.bin` and `pytorch_model-00002-of-00002.bin`. To load it into Ollama, it needs to be converted to GGUF format. Here's how to do it:

1. Install git-lfs: https://git-lfs.com/
2. Clone the Hugging Face model repository
3. Run the following command to convert the model to GGUF format:

```bash
python convert.py . --outfile gguf_model.bin
```

> [!info]
> Don't have the `convert.py` script? You can clone the llama.cpp repository and find it in the `scripts` folder.
> https://github.com/ggerganov/llama.cpp