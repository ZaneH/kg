---
title: Solidity Quirks
---

## Syntax Quirks

### Named return values

```solidity
// Named return values are supported like so.
function testReturn() public pure returns (uint256 tester) {
    tester = 3;
}
```

### Pure functions

While Solidity protects Solidity code from modifying state in pure functions, it does not protect against external calls that modify state. Check the [Shop](https://ethernaut.openzeppelin.com/level/0x691eeA9286124c043B82997201E805646b76351a) example from Ethernaut for an example of this.

## Hash Quirks

### Blockhash of the current block

```solidity
// Will always return 0x000...000 because it hasn't been mined.
bytes32 hash = blockhash(block.number);
```