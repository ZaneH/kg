---
title: Solana
date: 02-29-2024
tags: blockchain, crypto, solana
---

## Quickstart

- Rust is the primary language for Solana smart contracts.
- Regions of memory on-chain are called accounts.
    - Accounts [pay rent](https://solanacookbook.com/core-concepts/accounts.html#account-model) to be stored on-chain.
- PDAs are accounts that are derived from a seed and a program.
- CPI is the cross-program invocation, which is the way to call another program from a program.
- "Borsh" is the binary encoding format used by Solana.
    - Binary Object Representation Serializer for Hashing.
    - Think of it as a more efficient JSON.

## Guides

- [soldev.app](https://www.soldev.app/course/hello-world-program)
- [Solana Cookbook](https://solanacookbook.com/core-concepts/accounts.html#facts)
