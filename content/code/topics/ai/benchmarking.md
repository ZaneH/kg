---
title: Benchmarking AI Models
date: 03-16-2024
tags: ai, benchmarking
---

Choosing the right base model is pretty important and at the moment, I can't
find a comprehensive comparison between all of the popular models. As I go through
and experiment with them, I'll try to update this page with my findings.

> [!important] Define Benchmarking
> Benchmarking is quite difficult to get right. As a humble beginner in the AI
> field, I'm quite confident my benchmarks will be flawed. I'll do my best to
> make them interesting, fair, and informative.

## Methodology 1.0

Prefer the 13B/15B parameter model and/or the Q5_1 model if available.

- Ask a few standard questions (e.g. How many legs does a cat have?)
- Ask a few questions that are specific to the model (e.g. coding tasks, ridddles, text summarization)
- Compare the results and document its performance

## Models

- [[/code/topics/ai/models/starcoder2|StarCoder2]]: Coding LLM
    - "Supporting a context window of up to 16,384 tokens, StarCoder2 is the next generation of transparently trained open code LLMs."
- [[/code/topics/ai/models/deepseek-coder|DeepSeek Coder]]: Coding LLM
    - "DeepSeek Coder is trained from scratch on both 87% code and 13% natural language in English and Chinese."