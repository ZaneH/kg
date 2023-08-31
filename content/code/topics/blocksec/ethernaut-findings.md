---
title: Ethernaut Findings
---

This is a collection of my findings from the [Ethernaut](https://ethernaut.openzeppelin.com/) CTF. Here are some of the most important things I learned.

- CTFs are awesome.
- Learning to do math in JS and Solidity was challenging, but ultimately beneficial.
- Once things start to get harder, deploying a contract for each iteration is a pain. I started with Remix and the JS VM, but quickly moved to using `foundry` and forking the testnet. This was a huge time saver.
- Learning to write Solidity tests was a huge win. I've never written tests in Solidity before, but it makes a big difference.
- The `Re-entracy` challenge was the first one that really stretched my brain. After solving it, re-entry attacks make much more sense.