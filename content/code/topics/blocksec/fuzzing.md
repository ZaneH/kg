---
title: Fuzzing Smart Contracts
date: 09-09-2023
---

## Fuzzing

Fuzzing is a technique for finding bugs in software by providing random inputs. It's a great way to find bugs in smart contracts. After looking through a few professional audits, I've mostly seen fuzzers being used for "utility" functions rather than the core logic.

## Fuzzing with Echidna

[Echidna](https://github.com/crytic/echidna) feels like the AFL++ of smart contract fuzzers. Writing tests is pretty simple and there are plenty of options. Here's a simple setup:

```solidity
// TODO
```

## Fuzzing with Forge

Lots of smart contracts are already using Forge. `forge test` has fuzzing built-in so long as you provide an argument for the test. Here's a simple setup:

```solidity
function testFuzz_add(uint256 a, uint256 b) public {
    uint256 c = a + b;
    assertEq(c, a + b, "addition should be commutative");
}
```
