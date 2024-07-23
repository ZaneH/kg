---
title: Getting Better with Go
date: 07-22-2024
tags:
  - learning
  - go
---
After playing around with a bunch of languages, Go has certainly felt like one with staying power. It has a strong standard library, it has a simple and backwards compatible syntax, and goroutines/channels among other design decisions give it a nice [[language-feel]].

>[!info] Did you know?
>Go has a binary to serve the Go docs of every installed library. That's right, offline documentation, built-in 😎
>```
>$ go get golang.org/x/tools/cmd/godoc
>```

Thought getting *good* with Go and learning the idioms that make great software is not so simple. Through this page, I'm going to try sharing useful resources for learning Go as I go through it. Specific idioms can be found in [[code/languages/go-idioms/index]]
My goals are to learn Go well enough to use it as an API server, to write financial code that benefits from goroutines/channels and to learn the standard library enough to be useful.

Because I'm looking at Go as a more stable solution compared to using JavaScript, focusing on TDD seems like a good start.
- [Learn Go with tests](https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/hello-world)