---
title: Configure MacBook
date: 2020-07-22 13:00:00 -0500
categories: [Configuration, MacOS]
tags: [MacOS]
---


# Softwares

## VSCode


# Terminal

## Homebrew
1. Install homebrew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`
2. Install Joplin: `brew cask install joplin`
3. Install Emacs: `brew cask install emacs`
4. Install tmux: `brew install tmux`
5. Install wget: `brew install wget`
6. Install zsh-completions: `brew install zsh-completions`
7. Install zsh-syntax-highlighting: `brew install zsh-syntax-highlighting`

## iTerm
References:
- [Configuration of a beautiful (efficient) terminal and prompt on OSX in 7minutes](https://medium.com/@Clovis_app/configuration-of-a-beautiful-efficient-terminal-and-prompt-on-osx-in-7-minutes-827c29391961)

1. Install oh-my-zsh: `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
2. Add oh-my-zsh plugins: git, oxs, zsh-autosuggestions.
3. Import color scheme(Solarized Dark Higher Contrast) from online sources, and then set the color presets to be the selected one.
4. Use the default `robbyrussell` as the theme. Have tried `powerlevel9k` and `powerlevel10k`, not used to them. May try later.

## .zshrc

## ssh to servers
Follow my previous notes about server settings and git settings.
```bash
ssh-keygen -t rsa
# do the following for every cluster server
cat .ssh/id_rsa.pub | ssh x500@cluster 'cat >> .ssh/authorized_keys'
# do this for gcloud
ssh-add id_rsa
ssh -A account-name@external-ip
```
Then edit `.ssh/config` to create ssh shortcuts. Then I shall be able to connect to servers using `ssh cluster`.

## Git
Always remember to specify repository specific user.name and user.email if not my main account.

First, specify the global user.name and user.email to be my personal account. then for each repository, if a different account is used, then set repository-specific configurations.

```bash
# global configuration
git config --global user.name "<name>"
git config --global user.email "<email>"
# repository-specific configuration
git config user.name "<name>"
git config user.email "<email>"
```

Secondly, add `id_rsa.pub` to the SSH settings on github website and add shortcuts in `.ssh/config`. Then I shall be able to use git conveniently.

## Emacs
Following the instructions on my previous post [Emacs Configuration](https://yuyangyy.com/blog/posts/Emacs-Configuration/), and remove `elpy, flycheck, ein` packages. But the meta key problem has not been fixed yet, temporarily, just use `Esc`.

## Vim
I don't plan to use vim a lot, so just simply configure `.vimrc` as follows.
```bash
" Reference: https://www.shortcutfoo.com/blog/top-50-vim-configuration-options/

" indent options
set autoindent
set expandtab
set smarttab
set tabstop=4


" Search options
set hlsearch
set incsearch
set ignorecase
set smartcase

" Match options
set showmatch
set matchtime=5

" User Interface Options
set mouse=a
set ruler
set noerrorbells
set visualbell
set nocursorline
set number
set laststatus=2
```


## tmux settings
Install tmux plugin manager and plugins.
```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

Edit `.tmux.conf` file as follows.
```bash
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'

# enable mouse scrolling
set -g mouse on
```

Then reload tmux environment.
```bash
tmux source ~/.tmux.conf
```

# General

## Keyboard

### Shortcuts
`Cmd + Space`: I prefer Alfred to Spotlight, so I disabled this shortcut for Spotlight in `Keyboard -> Shortcuts -> Spotlight` and use it in Alfred.

### Key mappings
For MacBook Keyboard
- `Ctrl <-> Caps Lock`: I find it inconvenient to press Ctrl, but it is a frequently used key, so I swapped these two keys.

For my HP keyboard
- `Ctrl <-> Caps Lock`: swap it as well.
- `Option <-> Cmd`: I swap it on the key mappings and on the phisical keyboard.