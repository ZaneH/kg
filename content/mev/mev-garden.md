---
title: MEV Garden
---

## Introduction

Miner Extractable Value (MEV) is the profit a miner can make through their ability to arbitrarily include, exclude, or re-order transactions within the blocks they produce. This is a new phenomenon that has only been possible since the introduction of smart contracts and decentralized exchanges. It is a hot topic in the Ethereum community and is being actively researched.

## Motivation

I stumbled on [this tweet](https://twitter.com/BadPie1/status/1693684478638440525?s=20) that made ~80ETH from sniping shares on a new platform called friend.tech. Someone in the comments made another ~100ETH. This may not be classified as MEV, but it is the same idea in many respects.

Because this was a new platform that was gaining a lot of attention, the motivated searchers were able to find new opportunities and act on them. In hindsight, it was a very simple opportunity that was ripe for the taking.

- Read more about the [[mev/friend-tech-sniper|friend.tech snipers here]].

My motivation comes from these kinds of stories– developers who built a bot that automates a task to make a bunch of money. It never lasts forever, but opportunities like this are everywhere. I want to learn how to build these bots and find these opportunities.

## The Rundown

The space is competitive but there isn't a bot that can act on every opportunity. There are also actors who target specific bots and try to exploit them (see [Uncle Bandit Attacks](https://www.mev.wiki/attack-examples/uncle-bandit-attack).) This is a cat and mouse game that will continue to evolve. There is a lot of research and "alpha" to be found that increases the chances of success.

Much like security research, MEV "Searchers" have to think of ways to break and abuse systems. This is a specific mindset and requires creativity and patience. Once an opportunity is found, it's up to the searcher to build a bot that can act on it. This is a whole other skill that involves simulations, on-chain data parsing, mempools, transaction construction, and out of the box thinking.

## Unsorted Reference Material

- https://calblockchain.mirror.xyz/c56CHOu-Wow_50qPp2Wlg0rhUvdz1HLbGSUWlB_KX9o
- https://github.com/CoinCulture/evm-tools/blob/master/analysis/guide.md
- https://medium.com/@solidquant/first-key-to-building-mev-bots-your-simulation-engine-c9c0420d2e1
- https://ethresear.ch/
- https://timroughgarden.github.io/fob21/reports/r11.pdf
- https://twitter.com/evmcheb/status/1694614312046997924?s=20 | https://github.com/evmcheb/friendrekt
- https://github.com/evmcheb/ethers-rs-boilerplate
- https://medium.com/@solidquant/what-i-learned-from-a-month-of-intensive-mev-bot-study-38a4e357da0b
- https://medium.com/@solidquant/mev-templates-written-in-python-javascript-and-rust-ddd3d324d709
- https://www.blocknative.com/simulation-platform
- https://noxx.substack.com/p/mev-memoirs-into-the-arena-chapter-3e9?r=1bwfia&s=w
- https://github.com/DeGatchi/mev-template-rs
- https://github.com/refcell/subway-rs

## Researchers

- https://twitter.com/evmcheb
- https://twitter.com/rage_pit
- https://twitter.com/transmissions11
- https://twitter.com/mikeneuder
- https://twitter.com/DeGatchi