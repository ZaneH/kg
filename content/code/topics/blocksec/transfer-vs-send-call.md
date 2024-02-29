---
title: Transfer vs. Send vs. Call
date: 09-06-2023
---

### How to send Ether?

You can send Ether to other contracts by

- `transfer` (2300 gas, throws error)
- `send` (2300 gas, returns bool)
- `call` (forward all gas or set gas, returns bool)

### How to receive Ether?

A contract receiving Ether must have at least one of the functions below

- `receive() external payable`
- `fallback() external payable`

`receive()` is called if `msg.data` is empty, otherwise `fallback()` is called.

### Which method should you use?

`call` in combination with re-entrancy guard is the recommended method to use after December 2019.

Guard against re-entrancy by

- making all state changes before calling other contracts
- using re-entrancy guard modifier

```solidity title="SendingEther.sol"
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ReceiveEther {
    /*
    Which function is called, fallback() or receive()?

           send Ether
               |
         msg.data is empty?
              / \
            yes  no
            /     \
receive() exists?  fallback()
         /   \
        yes   no
        /      \
    receive()   fallback()
    */

    // Function to receive Ether. msg.data must be empty
    receive() external payable {}

    // Fallback function is called when msg.data is not empty
    fallback() external payable {}

    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}

contract SendEther {
    function sendViaTransfer(address payable _to) public payable {
        // This function is no longer recommended for sending Ether.
        _to.transfer(msg.value);
    }

    function sendViaSend(address payable _to) public payable {
        // Send returns a boolean value indicating success or failure.
        // This function is not recommended for sending Ether.
        bool sent = _to.send(msg.value);
        require(sent, "Failed to send Ether");
    }

    function sendViaCall(address payable _to) public payable {
        // Call returns a boolean value indicating success or failure.
        // This is the current recommended method to use.
        (bool sent, bytes memory data) = _to.call{value: msg.value}("");
        require(sent, "Failed to send Ether");
    }
}
```

### Try on Remix

- [SendingEther.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yMDsKCmNvbnRyYWN0IFJlY2VpdmVFdGhlciB7CiAgICAvKgogICAgV2hpY2ggZnVuY3Rpb24gaXMgY2FsbGVkLCBmYWxsYmFjaygpIG9yIHJlY2VpdmUoKT8KCiAgICAgICAgICAgc2VuZCBFdGhlcgogICAgICAgICAgICAgICB8CiAgICAgICAgIG1zZy5kYXRhIGlzIGVtcHR5PwogICAgICAgICAgICAgIC8gXAogICAgICAgICAgICB5ZXMgIG5vCiAgICAgICAgICAgIC8gICAgIFwKcmVjZWl2ZSgpIGV4aXN0cz8gIGZhbGxiYWNrKCkKICAgICAgICAgLyAgIFwKICAgICAgICB5ZXMgICBubwogICAgICAgIC8gICAgICBcCiAgICByZWNlaXZlKCkgICBmYWxsYmFjaygpCiAgICAqLwoKICAgIC8vIEZ1bmN0aW9uIHRvIHJlY2VpdmUgRXRoZXIuIG1zZy5kYXRhIG11c3QgYmUgZW1wdHkKICAgIHJlY2VpdmUoKSBleHRlcm5hbCBwYXlhYmxlIHt9CgogICAgLy8gRmFsbGJhY2sgZnVuY3Rpb24gaXMgY2FsbGVkIHdoZW4gbXNnLmRhdGEgaXMgbm90IGVtcHR5CiAgICBmYWxsYmFjaygpIGV4dGVybmFsIHBheWFibGUge30KCiAgICBmdW5jdGlvbiBnZXRCYWxhbmNlKCkgcHVibGljIHZpZXcgcmV0dXJucyAodWludCkgewogICAgICAgIHJldHVybiBhZGRyZXNzKHRoaXMpLmJhbGFuY2U7CiAgICB9Cn0KCmNvbnRyYWN0IFNlbmRFdGhlciB7CiAgICBmdW5jdGlvbiBzZW5kVmlhVHJhbnNmZXIoYWRkcmVzcyBwYXlhYmxlIF90bykgcHVibGljIHBheWFibGUgewogICAgICAgIC8vIFRoaXMgZnVuY3Rpb24gaXMgbm8gbG9uZ2VyIHJlY29tbWVuZGVkIGZvciBzZW5kaW5nIEV0aGVyLgogICAgICAgIF90by50cmFuc2Zlcihtc2cudmFsdWUpOwogICAgfQoKICAgIGZ1bmN0aW9uIHNlbmRWaWFTZW5kKGFkZHJlc3MgcGF5YWJsZSBfdG8pIHB1YmxpYyBwYXlhYmxlIHsKICAgICAgICAvLyBTZW5kIHJldHVybnMgYSBib29sZWFuIHZhbHVlIGluZGljYXRpbmcgc3VjY2VzcyBvciBmYWlsdXJlLgogICAgICAgIC8vIFRoaXMgZnVuY3Rpb24gaXMgbm90IHJlY29tbWVuZGVkIGZvciBzZW5kaW5nIEV0aGVyLgogICAgICAgIGJvb2wgc2VudCA9IF90by5zZW5kKG1zZy52YWx1ZSk7CiAgICAgICAgcmVxdWlyZShzZW50LCAiRmFpbGVkIHRvIHNlbmQgRXRoZXIiKTsKICAgIH0KCiAgICBmdW5jdGlvbiBzZW5kVmlhQ2FsbChhZGRyZXNzIHBheWFibGUgX3RvKSBwdWJsaWMgcGF5YWJsZSB7CiAgICAgICAgLy8gQ2FsbCByZXR1cm5zIGEgYm9vbGVhbiB2YWx1ZSBpbmRpY2F0aW5nIHN1Y2Nlc3Mgb3IgZmFpbHVyZS4KICAgICAgICAvLyBUaGlzIGlzIHRoZSBjdXJyZW50IHJlY29tbWVuZGVkIG1ldGhvZCB0byB1c2UuCiAgICAgICAgKGJvb2wgc2VudCwgYnl0ZXMgbWVtb3J5IGRhdGEpID0gX3RvLmNhbGx7dmFsdWU6IG1zZy52YWx1ZX0oIiIpOwogICAgICAgIHJlcXVpcmUoc2VudCwgIkZhaWxlZCB0byBzZW5kIEV0aGVyIik7CiAgICB9Cn0K)