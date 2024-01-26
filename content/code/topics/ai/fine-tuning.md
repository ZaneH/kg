---
title: Fine-Tuning LLMs
tags: ai, code
---

Finding info on fine-tuning is a bit of a mess. Each model has their own flavor for input. Often you'll just have to Google around to find the right format or a Python script that does it for you.

I have been on the lookout for alternatives to OpenAI, but I have yet to find a cheaper and easier alternative. I'll try to update this page if I find one.

## Locally

If you're like me, you want to do it locally. Unfortunately, this is quite an expensive task and it's not super simple yet. I'll try to update this page as I find better ways to do it. For now, OpenAI is my go-to.

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