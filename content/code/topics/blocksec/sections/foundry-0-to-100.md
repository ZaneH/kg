---
title: Foundry 0 to 100
date: 09-10-2023
---

- Start simple `forge init my-project`. You may need to restart your project once or twice.
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
- `vm.label(address(flashSwapper), "FlashSwapV2");` is a great way to label contracts.
- A full [cheatsheet can be found here](https://milotruck.github.io/blog/Foundry-Cheatsheet/).