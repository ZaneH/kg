---
title: Fine Tuning Llama3
date: 04-30-2024
tags: ai, fine-tuning
---

When Llama3 there was initially some confusion around fine-tuning it. People were saying that the earliest fine-tunes were objectively worse than the base model. From my current understanding, this is because Llama3 introduced some "special tokens" in the way it was trained and many of the existing tools didn't support this new format.

Today I stumbled on [Unsloth's repo](https://github.com/unslothai/unsloth). First impressions are very good, they have a complete notebook for preparing your dataset, and fine-tuning.

## Running Locally

The notebooks Unsloth provides are hosted on Colab. At first I thought I might port them to Jupyter to run locally, but then I learned you can run the Colab runtime locally! Using [this guide](https://research.google.com/colaboratory/local-runtimes.html) I was able to connect my GPU and RAM to my Colab notebook. This is a game changer for me, I can now run the fine-tuning process on my desktop withuot much change.

## Preparing Dataset

Each time I prepare a dataset, I create a folder with some Python scripts that do very simple file operations. I know there are tools to do this more efficiently, but I haven't quite understood them yet.

In the case of fine-tuning Llama3, I have the following scripts:

```bash
└── convert-to-jsonl.py
```

All this script does is read a CSV file, and creates JSON objects (1 per line) like this:

```json title="data.jsonl"
{"conversations": [{"from": "system", "value": "Write a tweet in all capital letters."}, {"from": "human", "value": "The topic is: Rap music"}, {"from": "gpt", "value": "I LOVE RAP MUSIIIIIIIIC"}]}
{"conversations": [{"from": "system", "value": "Write a tweet in all capital letters."}, {"from": "human", "value": "The topic is: Pokemon"}, {"from": "gpt", "value": "SNORLAX. THAT'S THE TWEET."}]}
```

Once I had ~400 lines of data like this, I knew it was enough to train the model. I imported it into the Colab space and changed the dataset code accordingly:

```diff
from datasets import load_dataset
-dataset = load_dataset("philschmid/guanaco-sharegpt-style", split = "train")
+dataset = load_dataset("json", data_files={"train": "./full.jsonl"}, split = "train")
dataset = dataset.map(formatting_prompts_func, batched = True,)
```

## Run the Fine-Tune

At some point in the Unsloth Colab notebook it starts the fine-tuning process. I was able to run a full fine-tune job locally on a 3060 (12GB VRAM) thanks to Unsloth's notebook. This is even better than using Cloud GPUs like I normally would. Once the fine-tune finished, there's a final step in the notebook if you want to manually export the model as `q5_k_m`:

```diff
-if False: model.save_pretrained_gguf("model", tokenizer, quantization_method = "q5_k_m")
+if True: model.save_pretrained_gguf("model", tokenizer, quantization_method = "q5_k_m")
```

Once this block runs, there's a new `model-unsloth.gguf` file in the explorer.

## Inferencing

Turns out, fine-tuning was half the battle. Figuring out how to run a fine-tuned Llama3 model was another task. vLLM and llama.cpp have the earliest support, so I opted for llama.cpp on my development machine. Using `./main` I was only able to get it working in interactive mode, but the `./server` is working like I was hoping.

```bash
./server --chat-template llama3 -m ~/Downloads/model-unsloth.Q5_K_M.gguf --port 8081
```

Visiting http://localhost:8081 brings you to a very retro looking page where you can put the system prompt and the user prompt into the text box and get a response. For my use case, I reset the context entirely on each request. This can now easily be integrated into an app using the API!

## Chat Templating

By far the worst part of this process in my experience has been chat templating. I found this[^1] which is provided by llama.cpp. It has some examples for popular chat templates. I think my rule of thumb is to wait for someone else to figure out how to make it work with fine-tuning and inferencing and then use their notebook with some modifications because it's quite time-consuming to get these chat templates working from scratch. That time could instead be spent creating high-quality datasets.

The chat template controls how your system prompt is added, how the user prompt is added and how stop tokens are managed. All of these are important to the text generation process.

If the chat template is wrong, you'll likely see artifacts from the training data in the output text. You might see 'system' at the end of every line for example.

[^1]: [Chat Template library](https://github.com/ggerganov/llama.cpp/wiki/Templates-supported-by-llama_chat_apply_template)