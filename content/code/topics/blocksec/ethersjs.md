---
title: Ethers.js Cheatsheet
date: 09-09-2023
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

## Create Wallet from Private Key

```js
let privateKey = "0xc678ef1aa456da65c6fc5861d44892cdfac0c6c8c2560bf0c9fbcdae2f4735a9";
let wallet = new ethers.Wallet(privateKey);

// Connect a wallet to mainnet
let provider = ethers.getDefaultProvider();
// provider is optional, but often needed
let walletWithProvider = new ethers.Wallet(privateKey, provider);
```

## Get Event Values

```js
// buyOne(...) is a func that emits TokenBought(...) event
const tx = await myContract.buyOne(myArgs);
const rc = await tx.wait();
const event = rc.events.find(event => event.event === 'TokenBought');
const [from, id, price] = event.args;
console.log(from, id, price);
```