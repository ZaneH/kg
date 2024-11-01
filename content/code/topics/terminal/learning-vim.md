---
title: Learning vim
tags: terminal, vim
date: 07-21-2024
---

## Why use vim?

If you use [[code/topics/os/linux|Linux]] frequently, you'll have to edit files frequently. In server environments, there is no GUI for VSCode to make those changes so we use `vim` often times. `vim` is a small text-editor, less than 50 MB and it runs completely in the terminal.

One of the best parts about vim is that it is *fast*. If you watch someone who has learned the shortcuts, it's faster than moving the mouse around and using a text editor in that way.

## Learning vim

Use `vimtutor`! It's a guide-book, but it's really well thought out for beginners. It comes installed alongside with vim. Wish I had used it sooner, especially to learn the basics of Visual mode.

To continuously get better requires deliberate practice and learning. vim doesn't come naturally until it does. Here's the stages or levels I've gone through since starting to learn vim.

- Level 1: Start with basic insert and delete commands (`i`, `A`, `d`)
- Level 2: Upgrade to vim motions (`dw`, `d$`, `y4`, `gg`)
- Level 3: Personalize vim, maybe upgrade to `nvim` for more useful extensions
	- Also useful to learn what vim experts are utilizing
- Level 4: Learn Visual and Visual Block modes for multi-cursor edits
	- Learn even more shortcuts here for navigating around code, jumping between parenthesis or going to function definitions
	- Deleting inside parenthesis and brackets (`di(`, `da{`)
	- Selecting around quote marks (`va"`/`va"c`)
- Level 5: Switch to emacs
