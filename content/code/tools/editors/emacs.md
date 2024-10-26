---
title: Emacs Quickstart
tags: code
date: 10-26-24
---

## Description

Emacs is a text editor that is hailed for its ability to be customized and many
people use it for their agenda, RSS feeds, code editing, and more. By extending
the base packages, vim keybindings could be enabled, LSPs can be configured, etc.

## Quickstart

I started with [Spacemacs](https://www.spacemacs.org/) which has 200+ packages
already configured. This instantly adds lots of keybinds and functionality to
emacs, and you'll have to decide if it's worth using.

Building a configuration from scratch (instead of using a distro like Spacemacs)
is often recommended for beginners to better understand what's happening
under the hood.

<!-- TODO: Insert image -->

## Terms

- [Projects](https://www.gnu.org/software/emacs/manual/html_node/emacs/Projects.html) - Just a folder.
- [Layers](https://www.spacemacs.org/doc/LAYERS.html) - A set of configurations that can be enabled/disabled to bring packages together
- [Modes](https://www.gnu.org/software/emacs/manual/html_node/emacs/Modes.html) - There are major and minor modes. Simply changes how text input affects the buffer.
- [Packages](https://www.gnu.org/software/emacs/manual/html_node/emacs/Packages.html) - Extending the base functionality of emacs

## Spacemacs Keybinds

>[!note]
>As you press keys, watch the menu that appears at the bottom of the screen to find more useful keybinds.

- <kbd>\<Space\> ?</kbd> - Opens all keybindings
- <kbd>,</kbd> - Opens the major chord menu
- <kbd>\<Alt\>+x</kbd> - Open emacs command menu
- <kbd>\<Space\> f s</kbd> - Save file
- <kbd>\<Space\> f t</kbd> - Open file tree
- <kbd>\<Space\> f e d</kbd> - Open emacs dotfile
- <kbd>\<Space\> f e R</kbd> - Reload emacs config
- <kbd>\<Space\> p f</kbd> - Find in project (fuzzy)
- <kbd>\<Space\> j =</kbd> - Auto-format code
- <kbd>\<Space\> w 2</kbd> - Split into a 2 window layout
- <kbd>\<Space\> w \<Tab\></kbd> - Navigate to next window
- <kbd>\<Space\> b b</kbd> - List all buffers
- <kbd>\<Space\> b x</kbd> - Close current buffer and window
- <kbd>\<Space\> T s</kbd> - Switch themes
- <kbd>\<Space\> q q</kbd> - Kill emacs
- <kbd>\<Space\> q f</kbd> - Kill current frame (leave emacs running)
- <kbd>\<Ctrl\>+c \<Ctrl\>+p a</kbd> - Add project to workspace
- <kbd>\<Ctrl\>+c \<Ctrl\>+p d</kbd> - Drop project from workspace

## Performance

Spacemacs and the OCaml layer added ~3s to my emacs startup time. Coming from
neovim, this was unacceptable and that's when I learned to run emacs as a daemon.

```bash
systemctl --user enable --now emacs
```

This command added emacs to my startup services. The idea is that we'll leave
emacs running all the time and connect with a client which is installed
as "Emacs (Client)" on my machine.

Instead of cold starting emacs, it will now have a daemon to instantly attach to.