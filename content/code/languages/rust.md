---
title: Learning Rust
date: 08-26-2023
tags: learning, rust
---

## Motivation

The motivation for learning Rust was slow to develop. There isn't really a reason I'd use Rust over another language until now. I've been interested in [[mev/garden|MEV bots]] the last few years and it's clear that Rust is the language of choice for the pros. Now that I have time to dive in, I'm excited to learn more about the language and the ecosystem.

## Initial Thoughts

- **08/26/23** The compile times are a bit annoying.
- The `Result<...>` pattern matching is very similar to Elixir.
    - `.unwrap()` is starting to make sense.
- The error messages are very helpful once you can parse them.
- Understanding the `Ok(())` syntax was useful.
- `tokio` was intimidating at first, but it's not so bad.
- I learned how to use `Mutex`. `Arc` is something I learned from [iOS](code/overview/mobile-programming).
- Starting to understand the build system + cargo. It's nice.
- [The Dev Method](https://www.youtube.com/watch?v=pGh-0cMvH5g&list=PLAJ-sYO1aGdxQ_skPPtJ7PlSAjTXM-atv) has a good playlist on Rust. It's definitely helping my understanding.
- **09/17/23** - I'm learning to use [Diesel](https://github.com/diesel-rs/diesel) next. Writing to a local SQLite database will be useful for some things I'm working on.
    - Also trying to understand when to use traits & enums.
    - Gave up on this project, writing SQL migrations with Rust is not fun!

## Solana

**02/26/2024** – Coming back to Rust for [[code/topics/blockchain/solana|Solana smart contract development]]. We'll see...

**12/15/2024** – That was fast. I certainly wasn't learning Rust that whole time but I've picked up quite a bit. Working with Solana has forced me to read and write Rust quite often. I'm still really interested in MEV and financial markets, and Rust is one of the gold standards for low-level programming in that field.

## Good to Know

- Don't forget your feature flags. Spent too long wondering why basic dependencies weren't working.
- Allow two different data types in a JSON field with Serde:

```rs
#[derive(Debug, Deserialize)]
#[serde(untagged)] // Don't forget this!
enum VariedValue {
    Name(String),
    Amount(u32),
}
```