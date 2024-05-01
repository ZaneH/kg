---
title: Fine-Tuning LLMs
tags: ai, code
date: 09-26-2023
---

Finding info on fine-tuning is a bit of a mess. Each model has their own flavor for input. Often you'll just have to Google around to find the right format or a Python script that does it for you.

I have been on the lookout for alternatives to OpenAI, but I have yet to find a cheaper and easier alternative. I'll try to update this page if I find one.

## Local Text Generation

If you're like me, you want to do it locally. This is a bit more complicated, but it's worth it if you like to tinker.

- [[/code/topics/ai/text-generation/fine-tuning|Fine-Tuning Locally]]
- [[/code/topics/ai/text-generation/fine-tuning-llama3|Fine-Tuning Llama3]] (Done)

## OpenAI

OpenAI has been *the easiest* in my experience for fine-tuning. You can start with just 10 samples in your `.jsonl` and you can get noticeable results.

OpenAI only charges you for the training time and the calls thereafter. If you're using it for a small project, you can get away with just a few dollars tops.

### Fine-Tuning with OpenAI

By going to the [fine-tuning page](https://platform.openai.com/finetune) you can upload your `.jsonl` file and start training. You can then copy the model ID to use in your code.

## Fine-Tuning Format

The format always looks similar (in my case):

```json title="tool_picker.openai.jsonl"
{"messages":[{"role":"system","content":"Your job is to decide which tool..."},{"role":"user","content":"Ok Billy, send that video of Peter falling on his knee"},{"role":"assistant","content":"{\"tool\": \"discord_post.youtube\", \"query\": \"Peter falling on his knee\"}"}]}
{"messages":[{"role":"system","content":"Your job is to decide which tool..."},{"role":"user","content":"Hey Billy, rock paper scissors"},{"role":"assistant","content":"{\"tool\": \"no_tool\"}"}]}
```

In other words:

- **system**: The prompt
- **user**: The input
- **assistant**: The expected output

```json
{
    "messages": [
        {
            "role": "system",
            "content": "{SYSTEM_PROMPT}"
        },
        {
            "role": "user",
            "content": "{USER_INPUT}"
        },
        {
            "role": "assistant",
            "content": "{EXPECTED_OUTPUT}"
        }
    ]
}
```

When working with open models, this format is different, but JSONL is still popular. There are libraries such as [HF's datasets](https://huggingface.co/docs/datasets/main/en/loading#json) which make working with datasets a breeze.

## Fine Tuning with Together.ai

On my main site, I have a page dedicated to [fine-tuning with Together.ai](https://together.ai/fine-tuning). It's a bit more complicated than OpenAI, but it has the added benefit of being able to fine-tune open-source models. This also means you can download the `.safetensors` and use them locally.

## Fine-Tuning Use Cases

### LLM as API

By training your LLM to produce JSON output, you can use it as an API. This is useful for almost any project. It can take arbitrary text and return a JSON object with the information you need or an action to take.

Example use cases:

- Read financial transactions and classify them
- Interpret voice commands
- Read a message and extract a certain piece of information

### LLM as a Chatbot

If you want to add some personality to your chatbot, this is the best way to do it. You can train your LLM to respond to certain prompts with a certain tone. You can also train it to respond to certain prompts with certain actions. More examples and more variations will make your chatbot more accurate.

### LLM as a Translator

You can train an LLM to translate between two programming languages or two formats. Simple prompts can be inaccurate, but with enough examples you can get a pretty good translator. This could save you hours of work.

## Experimental Use Cases

### Graph-Representation

LLMs are surprisingly good at generating/reading graphs. You can store a graph with nodes & edges in JSON and have the LLM modify it on the fly. This could be useful for a home assistant, a game, and other things that might branch out.

Using a graph removes a lot of the limitations of a simple input/output queue.

```json title="graph.json"
{
  "nodes": {
    "1": {
      "action": "input.text",
      "data": "Post a tweet about the weather in San Francisco"
    },
    "2": {
      "action": "data.wolfram_alpha",
    },
    "3": {
      "action": "confirm.edit",
    },
    "4": {
      "action": "output.tweet",
    }
  },
  "edges": [
    { "from": "1", "to": "2" },
    { "from": "2", "to": "3" },
    { "from": "3", "to": "4" }
  ]
}
```