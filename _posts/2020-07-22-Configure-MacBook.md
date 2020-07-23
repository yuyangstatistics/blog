---
title: Configure MacBook
date: 2020-07-22 13:00:00 -0500
categories: [Configuration, MacOS]
tags: [MacOS]
---

## Homebrew
1. Install homebrew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`
2. Install Joplin: `brew cask install joplin`
3. Install Emacs: `brew cask install emacs`
4. Install tmux: `brew install tmux`
5. Install wget: `brew install wget`
6. Install zsh-completions: `brew install zsh-completions`
7. Install zsh-syntax-highlighting: `brew install zsh-syntax-highlighting`

## Softwares

## iTerm
References:
- [Configuration of a beautiful (efficient) terminal and prompt on OSX in 7minutes](https://medium.com/@Clovis_app/configuration-of-a-beautiful-efficient-terminal-and-prompt-on-osx-in-7-minutes-827c29391961)

1. Install oh-my-zsh: `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
2. Add oh-my-zsh plugins: git, oxs, zsh-autosuggestions.
3. Import color scheme(Solarized Dark Higher Contrast) from online sources, and then set the color presets to be the selected one.
4. Use `powerlevel10k` as the theme.

## .zshrc


## General

### Keyboard

#### Shortcuts
`Cmd + Space`: I prefer Alfred to Spotlight, so I disabled this shortcut for Spotlight in `Keyboard -> Shortcuts -> Spotlight` and use it in Alfred.

#### Key mappings
For MacBook Keyboard
- `Ctrl <-> Caps Lock`: I find it inconvenient to press Ctrl, but it is a frequently used key, so I swapped these two keys.

For my HP keyboard
- `Ctrl <-> Caps Lock`: swap it as well.
- `Option <-> Cmd`: I swap it on the key mappings and on the phisical keyboard.