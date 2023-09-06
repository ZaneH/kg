---
title: Ethers.js Cheatsheet
---

## Advance Time

```js
await ethers.provider.send("evm_increaseTime", [5 * 24 * 60 * 60]); // 5 days
```

## Send Tx as Signer

```js
const mySigner = await ethers.getSigners()[0];
await myContract.connect(mySigner).myFunction();
```