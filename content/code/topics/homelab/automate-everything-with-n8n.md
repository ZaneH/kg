---
title: Automate everything with n8n
tags: [ai, automation]
---

n8n has easily over 100+ integrations and functionalities than can be tied together in a graph editor. It comes with handy triggers so instead of messing with crontab, I can just create a new workflow in n8n.
Very pleased to see they have integrations for all kinds of LLM services including Ollama.

Some of the features are paywalled, namely:
- Variables
- Storing credentials in a vault
Third party nodes can be installed when needed.

## First Use Cases

- Created a good morning bot that DM's Matrix and Discord with my daily agenda.
- Read group chat history and summarize with an LLM.
- A workflow that takes a Google Sheet, feeds one of the columns through an LLM to generate synthetic data in bulk.