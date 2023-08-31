---
title: MEV Garden
---

## Introduction

Maximal Extractable Value (MEV) is the profit made by arbitrarily including, excluding, or re-ordering transactions on the blockchain. This is a new phenomenon that has only been possible since the introduction of smart contracts and decentralized exchanges. It is a hot topic in the Ethereum community and is being actively researched.

Lots of the professionals are using Rust to build their bots. This is because Rust is faster than other languages and speed is pretty important when it comes to PvP situations.

- [[code/languages/rust|Learning Rust]]

## Motivation

I stumbled on [this tweet](https://twitter.com/BadPie1/status/1693684478638440525?s=20) that made ~80ETH from sniping shares on a new platform called friend.tech. Someone in the comments made another ~100ETH. This may not be classified as MEV, but it is the same idea in many respects.

Because this was a new platform that was gaining a lot of attention, the motivated searchers were able to find new opportunities and act on them. In hindsight, it was a very simple opportunity that was ripe for the taking.

- Read more about the [[mev/friend-tech-sniper|friend.tech snipers here]].

My motivation comes from these kinds of stories– developers who built a bot that automates a task to make a bunch of money. It never lasts forever, but opportunities like this are everywhere. I want to learn how to build these bots and find these opportunities.

## The Rundown

The space is competitive but there isn't a bot that can act on every opportunity. There are also actors who target specific bots and try to exploit them (see [Uncle Bandit Attacks](https://www.mev.wiki/attack-examples/uncle-bandit-attack).) This is a cat and mouse game that will continue to evolve. There is a lot of research and "alpha" to be found that increases the chances of success.

Much like security research, MEV "Searchers" have to think of ways to break and abuse systems. This is a specific mindset and requires creativity and patience. Once an opportunity is found, it's up to the searcher to build a bot that can act on it. This is a whole other skill that involves simulations, on-chain data parsing, mempools, transaction construction, and out of the box thinking.

## Unsorted Material

- [friendrekt by evmcheb](https://twitter.com/evmcheb/status/1694614312046997924?s=20)
    - [GitHub repo](https://github.com/evmcheb/friendrekt)

---

## Introduction

- [The 0 to 1 Guide for MEV](https://calblockchain.mirror.xyz/c56CHOu-Wow_50qPp2Wlg0rhUvdz1HLbGSUWlB_KX9o)
- [What I learned from a month of intensive MEV bot study (by @SolidQuant)](https://medium.com/@solidquant/what-i-learned-from-a-month-of-intensive-mev-bot-study-38a4e357da0b)
- [Transaction prediction through EVM tracing (by @SolidQuant)](https://medium.com/@solidquant/how-i-spend-my-days-mempool-watching-part-1-transaction-prediction-through-evm-tracing-77f4c99207f)
- [Simulate DEX trades](https://medium.com/@solidquant/first-key-to-building-mev-bots-your-simulation-engine-c9c0420d2e1)

### Templates

- [Rust sandwich bot template](https://github.com/refcell/subway-rs)
- [MEV templates in Python, Javascript, and Rust (by @SolidQuant)](https://medium.com/@solidquant/mev-templates-written-in-python-javascript-and-rust-ddd3d324d709)
- [Rust MEV template](https://github.com/DeGatchi/mev-template-rs)
- [ethers-rs boilerplate](https://github.com/evmcheb/ethers-rs-boilerplate)

## Diving Deeper

- [Using assembly to reduce your gas costs (by @SolidQuant)](https://medium.com/@solidquant/up-your-mev-game-by-using-assembly-93c31b06cf96)
- [Huff Guide - EVM Basics](https://docs.huff.sh/tutorial/evm-basics/#technical)
- [Sothis - Replay and track historical state](https://github.com/rainshowerLabs/sothis)
- [Decoding calldata, bytecode, MEV bots, etc. (deep dive)](https://mirror.xyz/wschwab.eth/CjODHmpDMTbZsAACyFJyFJkB3YakZqH8KUko4AOTMkA)
- [Unearthing Alpha through Decompiled Contracts](https://noxx.substack.com/p/mev-memoirs-into-the-arena-chapter-3e9?r=1bwfia&s=w)
- [MEV on L2 paper](https://timroughgarden.github.io/fob21/reports/r11.pdf)

---

## CTFs and Challenges

- [Huff challenges (easy to hard)](https://github.com/RareSkills/huff-puzzles)
- [Ethernaut - Smart contract CTF (easy to hard)](https://ethernaut.openzeppelin.com/)

---

## AMMs

- [Rust lib for various AMMs](https://github.com/darkforestry/amms-rs/tree/main)
- [Uniswap v3 math blog](https://blog.uniswap.org/uniswap-v3-math-primer)
- [Uniswap v3 math videos](https://www.youtube.com/@smartcontractprogrammer/videos)

---

## Simulation Services

- [blocknative.com](https://www.blocknative.com/simulation-platform)
- [tenderly.co](https://tenderly.co/)

---

## Static Analysis

- [Slither - Static analyzer for Solidity](https://github.com/crytic/slither)
- [Dedaub byecode decompiler](https://library.dedaub.com/ethereum/address/0xbadc0defafcf6d4239bdf0b66da4d7bd36fcf05a/decompiled)
- [ethervm.io decompiler](https://ethervm.io/decompile/0xDd6Bd08c29fF3EF8780bF6A10D8b620A93AC5705)
    - Helpful for harder to read contracts

---

## Web Tools

### Encoding

- [ETH Calldata Decoder](https://calldata-decoder.apoorv.xyz/)
- [Keccak-256 Tool](https://emn178.github.io/online-tools/keccak_256.html)

### Explorers

- [ETHtx](https://ethtx.info/mainnet/0xb52668345b575b2baedd2801d13b6bac25fc594ec7e8ed1776f47d1200e3ebb9/)

---

## Bootcamps and Academies

- [yAcademy fellowship](https://yacademy.dev/fellowships/)

---

## Researchers

- [@evmcheb](https://twitter.com/evmcheb)
- [@rage_pit](https://twitter.com/rage_pit)
- [@transmissions11](https://twitter.com/transmissions11)
- [@mikeneuder](https://twitter.com/mikeneuder)
- [@DeGatchi](https://twitter.com/DeGatchi)
- [@0xmouseless](https://twitter.com/0xmouseless)

---

## Communities

- [ETH Research Forum](https://ethresear.ch/)

---

## Thoughts While Practicing
- A tool to export all enums/structs from a Solidity file would be nice
- MEV feel more like a game than a profession. During my short journey, I think I've noticed what I really enjoy– it's the puzzle and the reward.
    - [[code/topics/blocksec/garden|Whitehat]] security research looks quite appealing. There's a lot of funds to protect and the space is still young. I think I'll start looking into this more.