---
title: Solidity Quirks
date: 09-06-2023
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

While Solidity protects internal code from modifying state in pure functions, it does not protect against external calls that modify state. Check this [writeup for the Ethernauts "Shop" challenge](https://coinsbench.com/21-shop-ethernaut-explained-107cc17dedba) to see how this can be exploited.

## Hash Quirks

### Blockhash of the current block

```solidity
// Will always return 0x000...000 because it hasn't been mined.
bytes32 hash = blockhash(block.number);
```

## Value Quirks

### Using `msg.value` in loops

Be careful of using `msg.value` in loops. If there aren't proper checks, a `buyMany()` may not work as expected.

```solidity title="BuggyBuy.sol"
/// Buy many NFTs at once. Payable.
function buyMany(uint256[] calldata tokenIds) external payable nonReentrant {
    for (uint256 i = 0; i < tokenIds.length; i++) {
        _buyOne(tokenIds[i]);
    }
}

/// Buy one NFT.
function _buyOne(uint256 tokenId) private {
    uint256 priceToPay = offers[tokenId];
    // NOTE: `msg.value` is not decremented in the loop
    if (msg.value < priceToPay)
        revert InsufficientPayment();

    _token.safeTransferFrom(_token.ownerOf(tokenId), msg.sender, tokenId);
    payable(_token.ownerOf(tokenId)).sendValue(priceToPay);
}
```