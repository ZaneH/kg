---
title: Whitehat Blockchain Security
date: 09-06-2023
---

## Sections

- [[code/topics/blocksec/sections/foundry-0-to-100|Foundry 0 to 100]]
- [[code/topics/blocksec/sections/gas-optimizing|Gas Optimizing]]
- [[code/topics/blocksec/sections/news|News]]
- [[code/topics/blocksec/sections/trial-by-fire|Trial by Fire]]
- [[code/topics/blocksec/sections/deeper-readings|Deeper Readings]]
- [[code/topics/blocksec/sections/past-vulnerabilities|Past Vulnerabilities]]

## Common Questions

- [[code/topics/blocksec/transfer-vs-send-call|Transfer vs. Send vs. Call]]
- Understanding Calldata
    - [EVM byte storage in Solidity](https://noxx.substack.com/p/evm-deep-dives-the-path-to-shadowy-3ea)

## Timeline

- [[code/topics/blocksec/solidity-quirks|Solidity Quirks]]
- Day 4: I'm getting familiar with all of the tools. With my current knowledge, I'll only be able to spot very specific bugs. I need to broaden my knowledge and read more code. I'm also realizing math will be an important skill in this field.
    - Finding interesting contracts to analyze takes time. Some kind of parser would be nice.
        - Reading through "internal transactions" is a good start.
        - GitHub has also been an ok source.
- [[code/topics/blocksec/fuzzing|Fuzzing]] has been helpful and fun.
- [[code/topics/blocksec/ethersjs|Ethers.js]] is not my first choice, but it's popular. Damn Vulnerable DeFi taught me a lot about Ethers.js.
- Day 14: Seems like everyone working in the space is pretty anonymous... I may end up doing the same.
    - By now, I've written a basic parser to find interesting contracts.
    - I've gone through Ethernaut and Damn Vulnerable DeFi. Really helped me in learning Solidity and Yul. Lots of clever solution writeups to discover.
    - EVM is no longer a mystery, it's just a really cool machine.
    - Currently thinking about specializing and auditing with [code4rena](https://code4rena.com/). Still testing the waters.