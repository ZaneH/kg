---
title: friend.tech Sniper
tags: mev, bots, crypto
date: 08-26-2023
---

## Introduction

I stumbled on [this tweet](https://twitter.com/BadPie1/status/1693684478638440525?s=20) that made ~80ETH from sniping shares on a new platform called friend.tech. Someone in the comments made another ~100ETH.

After some further digging, [this tweet](https://twitter.com/evmcheb/status/1694614245516955709?s=20) explained how it was done. As an exercise, I decided to further elaborate on the flaw and how people used it to make some serious money. There's also a repo I'm using to recreate evmcheb's friendrekt repo [here](https://github.com/buidlcat/friendrekt).

## The Flaw

As mentioned in the tweet thread, the flaw is due to a mempool leak on the nodes that friend.tech uses. This means that the nodes are leaking transactions that are not yet included in a block. Because of this, people can "back-run" transactions and place their purchase right after the target transaction.

>[!note]
>Back-running is a strategy that's most often used when being first is important. In this case, the first person to buy a share gets the best price. Some common strategies to have the best chance of being included next:
>
>- Match the gas price of the target transaction
>    - Increases the odds of being placed near the target transaction
>- Spam the mempool with the same transactions
>    - Use a smart contract
>        - Broadcast a function call for preloaded accounts to spam the mempool
>    - Revert txs if they don't match the criteria
>
>- Further reading:
>    - https://www.mev.wiki/attack-examples/back-running
>    - https://amanusk.medium.com/the-fastest-draw-on-the-blockchain-bzrx-example-6bd19fabdbe1

Unfortunately, back-running is no longer possible on the nodes that friend.tech uses. It was patched with [this PR](https://github.com/ethereum-optimism/op-geth/pull/118). The PR explains that "op-stack chains can leak tx pool contents on shared nodes." And because friend.tech was using a shared node, the mempool contents were available to those with the alpha.

Below is a snippet from [friendrekt/main.rs](https://github.com/evmcheb/friendrekt/blob/0a0045152a057dfb59d8fd211a1631ceec5bb6e7/friendrekt-rs/src/main.rs#L255) which shows how the mempool was being read.

```rust title="friendrekt-rs/main.rs"
// for reading pending txs
let mempool_client = Provider::<Ws>::connect("wss://base-mainnet.blastapi.io/{PROJECT_ID}").await?;
// for sending txs
let fasthttp = fasthttp::FastHttp::new("https://mainnet-sequencer.base.org/".to_string());
...
// subscribe to pending txs (alpha for back-running)
let mempool_stream = mempool_client.subscribe_pending_txs().await.unwrap();
...
```

If you run this code now, it will return `pending tx filters are disabled` because of the patch. It was not intentional to leak the mempool contents, but it was a side effect of the (default) configuration the friend.tech nodes were using.

With all of this known, how can it be used to make money? Well the goal is to find new people who are joining friend.tech that have a large following. These people will be likely to have profitable shares once they advertise it to their following. The goal is to find these people and back-run their transactions to be the first buyer.

If that can be done, the shares can be sold back to the market for a profit.

## The Exploit

By using [friendrekt by evmcheb](https://github.com/evmcheb/friendrekt) we can understand how a developer could use all of this to execute on this strategy. The bot's flow can be explained in the following steps:

1. Subscribe to pending transactions (no longer possible.)
    - Alternatively, you can subscribe to new blocks and check the transactions in the block. This is not as effective as the original method.
2. Check for pending transactions that are relevant and asynchronously fetch Twitter followers for the ETH address. This is done by first using [prod-api.kosetto.com](https://web.archive.org/web/20230827020122/https://prod-api.kosetto.com/users/0xa9c8e1bb3b13264410da8923cfe48e795d1f1d60) which is operated by friend.tech. Then [[code/overview/web-scraping|scrape]] Twitter for their follower count.
3. Check if the transaction is a share purchase.
    - If it is, check the `shareSupply` to see if it's worth targeting.
    - A `supply_limit` is set at different levels depending on the number of followers. If the amount of shares bought is past the `supply_limit`, it's not worth targeting.
4. If the shares are worth targeting, back-run the transaction
    - This is done with a smart contract called `Sniper.sol`.
    - In the friendrekt demo, I don't believe there is any back-running happening in its current state. But a lot of the ideas are there.

## Thoughts

- <s>I imagine the `FIFOCache` should be more than 10 entries. 100 or 1,000 wouldn't take that much more memory and would increase the odds of finding a target quickly.</s>
    - Correction: The `FIFOCache` is being used to deduplicate WebSocket transactions, not store Twitter followers. The `HashMap` is used to store Twitter followers. [(Source)](https://github.com/evmcheb/friendrekt/issues/1#issuecomment-1695455611)
- The `supply_limit` is a good idea, but now that everyone has this knowledge, additional logic should be added to optimize for profit.
- The original code looks like it was written in a rush. I'm no Rust expert, but I think it could be improved.
- friend.tech was quickly "saturated" by bots who knew about the repository that I based this article on. That's interesting. There are also adversaries who are trying to drain bots. Interesting.
- I now realize that the `&relay_tx_sig` is an event from the L2 bridging mechanism. I think it's used in preparation for someone signing up to friend.tech.
- $BASE is a new chain. This brings new opportunity and I can understand why this knowledge is not being advertised (shoutout to [@bertcmiller for advertising this too](https://twitter.com/bertcmiller/status/1695050338171015644?s=20).) There are people making serious beans on-chain. I thought L2 MEV was going to be impossible, but I was wrong. I'm excited to see what happens next.
- The goal is to find "long tail" MEV opportunities. This is a good example of that, but only if you were early. I think there are more opportunities like this out there. I'm going to keep looking. There are some good ideas I've found to find other long tail opportunities:
    - Look for transactions with low miner fees (these are less competitive MEV strategies.)
    - Look for transactions with `0x******` function calls. These are likely MEV bots.
    - Read about new protocols and try to understand if they have MEV opportunities.