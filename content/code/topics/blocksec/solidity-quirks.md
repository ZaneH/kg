---
title: Solidity Quirks
---

## Syntax Quirks

```solidity
// Named return values are supported like so.
function testReturn() public pure returns (uint256 tester) {
    tester = 3;
}
```

## Hash Quirks

```solidity
// Will always return 0x000...000
bytes32 hash = blockhash(block.number);
```