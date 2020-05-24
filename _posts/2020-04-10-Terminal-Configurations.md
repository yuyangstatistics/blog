---
title: Terminal Configurations
date: 2020-04-10 12:28:12 -0500
categories: [Tools]
tags: [zsh]
---

## iTerm2


## zsh
After seeing several posts talking about the benefits of zsh over bash, I finally decided to switch from bash to zsh. In order to not lose key feature before, I did the following configurations inside `~/.zshrc`.

- I used [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) to manager my zsh configuration. I chose the dafault `robbyrussell` theme and added a few important plugins: osx, git, zsh-autosuggestions. I don't want to be surrounded with so many features that I would not use frequently, and the cost to learn those shortcuts is a bit high, so I just included these three plugins so far.
- Remember to add `export PATH=$HOME/bin:/usr/local/bin:$PATH` if you also come from bash.
- Move alias settings in `~/.bash_aliases` to `~/.zshrc`.
- Add `alias reload="source ~/.zshrc"` to quickly reload the settings.
- After switching, the default python interpreter would be python2.7, so add the path of python 3. Note that for zsh, we can use an easier way as follows to add to PATH.
  ```zsh
  path+=("/Library/Frameworks/Python.framework/Versions/3.7/bin")
  path+=('/Users/yuyang/.local/bin')
  export PATH
  ```
- Move the conda initialization file to set the default python environment to be conda.

### OSX plugin
Reference:
- [OXS plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/osx)

Among the commands, I found three of them very helpful.
- `tab`: open the current directory in a new tab.
- `split_tab`: split the current terminal tab horizontally.
- `vsplit_tab`: split the current terminal tab vertically.
