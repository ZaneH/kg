---
title: Solana MEV
tags: solana, mev, bots, crypto
---


## Beginners

> [!warning] When using old code examples, **be sure** to update your `Cargo.toml` file with the latest packages to prevent any issues.

- [Start here](https://www.soldev.app/course/hello-world-program)
- [Then understand serialization](https://github.com/Unboxed-Software/solana-course/blob/main/content/serialize-instruction-data.md)
    - Gives a great introduction to how Solana programs are executed and how to encode instructions.
    - Interactive examples included.
- [Then understand instruction data](https://www.soldev.app/course/deserialize-instruction-data)
    - Focuses heavily on the Rust side of things.
    - Goes over impl, structs, and enums.
    - Real-world example included.
    - This is without using the Anchor framework.
    - Will be useful for understanding how to decode transaction data in real-time.

> [!warning] Friendly reminder to update your Solana dependencies when using old code samples, **be sure** to update the `Cargo.toml` file with the latest packages to prevent any weird issues! This has cost me many hours by now :)

## Troubleshooting

This issue happens when you try to build a project with outdated dependencies.

```
error: package `bumpalo v3.15.4` cannot be built because it requires rustc 1.73.0 or newer, while the currently active rustc version is 1.72.0-dev
Either upgrade to rustc 1.73.0 or newer, or use
cargo update -p bumpalo@3.15.4 --precise ver
where `ver` is the latest version of `bumpalo` supporting rustc 1.72.0-dev
```

## Extra Resources

- [Solana Developer Guides](https://solana.com/developers/guides)