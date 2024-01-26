---
title: AI Assisted Programming
tags: ai, code
---

## Related Pages

- [Fine-Tuning](/code/topics/ai/fine-tuning)

## The Rundown

This note will certainly be outdated the quickest. ChatGPT is less than a year old and the field is still moving quickly. This new bread of AI is the first time I (and many others) have integrated AI into the developer's workflow. Over the last year I paid for GitHub's Copilot service which in the beginning was immensely helpful. The general consensus seems to be that it has gotten worse over the last few months. I think this is part of the process, and we'll see a lot of improvement over the next few years.

From personal experience, Python and JavaScript are where Copilot excel. Given that they're some of the most popular programming languages, it makes sense. It does mean however that Copilot is much less helpful for a language like Elixir for example.

---

## Code Generation

The key selling point is that Copilot can generate code for you. This is a huge time saver, and I've found it to be very helpful. I've also found that it can introduce very subtle bugs.

The best way to use Copilot (in my current opinion) is to never accept the suggestion, but rather read it, understand it, and then write it yourself. This way you can scrutinize each character before committing it to your codebase.

Another good practice is to give Copilot cues. For example, if you're writing a new function, start with the function signature and a docstring. Copilot will then be able to infer what you're trying to do and generate the code for you.

---

## Documentation

If you ask the AI to document your code, there's a good chance it'll be able to generate documentation for it that's complete, easy to understand, and accurate. This is a huge win for developers. I've always been a fan of documentation, but it's a lot of work to maintain. I think this is a great use case for AI.

In my own experience, writing documentation for a new product has a big problem: OpenAI doesn't know about your product more than likely. [Obsidian has been useful for taking existing content](#obsidian) and generating documentation from it.

---

## Unit Tests

Copilot has also been helpful in writing unit tests. It typically works best if the function is documented. You can use comments to suggest what kinds of tests you want to write, and most of the time, it'll just generate the tests for you.

When working with very specific tooling, I've noticed that Copilot can get confused. Using `pytest`'s monkeypatch modules often produced bad code for example.

---

## ChatGPT as a Fallback

I've found that ChatGPT is a great fallback when Copilot doesn't know what to do. Sometimes it's easier to have a conversation with ChatGPT than trying to get the right code out of Copilot.

I've also found that ChatGPT is naturally better at explaining things than Copilot, which if you take the time to understand, can be very helpful.

### ChatGPT Template

Every time I bring code to ChatGPT, I use the same template. I noticed that if you include the question at the end, it might miss the question entirely if the code snippet is long enough, so placing it at the beginning seems to work best.

````
I need this thing done with this tool, can you generate the code for me?
Here's my current code:

```
<include some code here>
```
````

>[!note]
>ChatGPT has a similar issue to GitHub Copilot where it likes to make up things if it doesn't have enough knowledge on the subject. Keep this in mind.

---

## Obsidian

Obsidian can be connected to ChatGPT. Why is that useful? Well you can create canvases is Obsidian and connect nodes of information to "train" ChatGPT. This is a great way to build up a knowledge base for ChatGPT to use. It requires an API key from OpenAI, but it's worth it if this sounds interesting to you.

### Community Plugins

- [Chat Stream](https://obsidian.md/plugins?id=chat-stream)
- [Link Exploder (Optional)](https://obsidian.md/plugins?id=link-exploder)

You will need to enable and configure these plugins in the settings of your Obsidian vault. Create a canvas and start adding notes/pages to it. Point these "inputs" to your prompt and with the prompt note selected, press <kbd>Alt+Shift+G</kbd> to generate a response.

Link Exploder is an optional "nice to have" plugin. It will automatically expand a page and all of its children into a new canvas. This is useful if you already have an existing knowledge base in Obsidian. **Note:** By default, the arrows are backwards from what Chat Stream expects.