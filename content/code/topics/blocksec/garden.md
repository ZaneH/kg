---
title: Whitehat Blackchain Security
---

## Foundry 0 to 100

- Start simple. You may need to restart your project once or twice.
- Learn to create interfaces for external contracts and use them.
- Good to know:
    - `hex"..."` is a `bytes` literal. It's the easiest way to create bytes from hex.
    - Do not initialize your contract in the `setUp()` function. It causes bugs. Currently I initialize the contract in each test.
- Learn to test with `forge test -vvvvv` (full trace)
    - Fork the network with `vm.createSelectFork(...)` in your `setUp()`
        - Optionally, provide a block number for faster tests.
    - Use the `--debug` flag to attach a debugger.
    - Use `vm.breakpoint("a")` to set a breakpoint.
    - Use `vm.startPrank(...)` and `.stopPrank()` to set `msg.sender`
- Learn to use `console2.log` and its variants (`console2.logBytes32`, etc.)
    - They can be used inside of tests and contracts.
- Learn to use Chisel to quickly prototype a script.
    - Import this script into a foundry project and run it with `forge script scripts/MyScript.s.sol --fork-url ... -vvvvv`
    - This provides similar functionality to smart contracts, but acts more like EOA or an "ETH REPL."
    - Use `!help` to see available commands.

## News

- [rekt.news](https://rekt.news/)

## Trial by Fire

- [Discover the 0xbadcode](https://medium.com/immunefi/0xbadc0de-mev-bot-hack-analysis-30b9031ff0ba)
- [Ethernaut](https://ethernaut.openzeppelin.com/)
    - See what I learned from Ethernaut [here (no spoilers)](/code/topics/blocksec/ethernaut-findings.md)
- [Damn Vulnerable DeFi Foundry](https://github.com/nicolasgarcia214/damn-vulnerable-defi-foundry)

## Common Questions

- [[code/topics/blocksec/transfer-vs-send-call|Transfer vs. Send vs. Call]]
- Understanding Calldata
    - [EVM byte storage in Solidity](https://noxx.substack.com/p/evm-deep-dives-the-path-to-shadowy-3ea)

## Deeper Readings

- [Bit Manipulation](https://hackmd.io/@fiveoutofnine/Skl9eRbX9)