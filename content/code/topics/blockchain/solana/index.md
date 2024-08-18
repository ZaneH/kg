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
- Tokens on Solana come in two flavors currently: SPL and "Token-2022".
    - SPL tokens are the standard token format.
    - "Token-2022" is a more advanced token format and we don't see them much in the current environment.
- SPL tokens use the [Token program](https://spl.solana.com/token).
    - This is an on-chain program that manages token accounts. There are many of these pre-deployed programs on Solana (e.g. Token-2022 program, SPL associated token account program, address lookup table program)
- Lots of guides/docs are incomplete or outdated. Expect to do a lot of digging and experimentation.
	- GPT-4 has a decent grasp of using `@solana/web3.js` and tangential libraries
## Guides

- [soldev.app](https://www.soldev.app/course/hello-world-program)
- [Solana Cookbook](https://solanacookbook.com/core-concepts/accounts.html#facts)

## Libraries

### JavaScript
- ed25519-hd-key - Great when dealing with seed phrases
- bip39
- @solana/web3.js