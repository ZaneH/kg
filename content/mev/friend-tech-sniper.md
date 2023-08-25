---
title: friend.tech Sniper
tags: alpha, back-running, mempool, mev
---

## Introduction

I stumbled on [this tweet](https://twitter.com/BadPie1/status/1693684478638440525?s=20) that made ~80ETH from sniping shares on a new platform called friend.tech. Someone in the comments made another ~100ETH.

After some further digging, [this tweet](https://twitter.com/evmcheb/status/1694614245516955709?s=20) explained how it was done. As an exercise, I decided to further elaborate on the flaw and how people used it to make some serious money.

## The Flaw

As mentioned in the tweet thread, the flaw is due to a mempool leak on the nodes that friend.tech uses. This means that the nodes are leaking transactions that are not yet included in a block. Because of this, people can "back-run" transactions and place their purchase right after the target transaction.

- Further reading on back-running
    - https://www.mev.wiki/attack-examples/back-running
    - https://amanusk.medium.com/the-fastest-draw-on-the-blockchain-bzrx-example-6bd19fabdbe1

>[!note]
>Back-running is a strategy that's most often used when being first is important. In this case, the first person to buy a share gets the best price. Some common strategies to have the best chance of being included next:
>
>- Match the gas price of the target transaction
>    - Increases the odds of being placed near the target transaction
>- Spam the mempool with the same transactions
>    - Use a smart contract
>        - Broadcast a function call for preloaded accounts to spam the mempool
>    - Revert txs if they don't match the criteria

Unfortunately, back-running is no longer possible on the nodes that friend.tech uses. It was patched with [this PR](https://github.com/ethereum-optimism/op-geth/pull/118). The PR explains that "op-stack chains can leak tx pool contents on shared nodes." And because friend.tech was using a shared node, the mempool contents were available to those with the alpha.

- todo: Find exactly how that mempool was being accessed (WS to what URL?)

With all of this known, how can it be used to make money? Well the goal is to find new people who are joining friend.tech that have a large following. These people will be likely to have profitable shares once they advertise it to their followers. The goal is to find these people and back-run their transactions.

## The Exploit

