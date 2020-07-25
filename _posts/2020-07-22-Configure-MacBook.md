---
title: Configure MacBook
date: 2020-07-22 13:00:00 -0500
categories: [Configuration, MacOS]
tags: [MacOS]
---


# Softwares

## VSCode

### Plugins
```
Python, Remote Development, C/C++, Markdown Preview Enhanced, 
```

### Keyboard Shortcuts
References
- [VS Code Keyboard shortcuts for macOS](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)

Display
- `Cmd+B`: toggle sidebar visibility
- `Cmd+Shift+E`: show explorer
- `Cmd+Shift+X`: show extensions

### Remote Development
References
- [Remote Development using SSH](https://code.visualstudio.com/docs/remote/ssh)

Install the Remote Development extension pack in VS Code, and this would enable us to use VS Code to edit remote files.

- Open VS Code, press `F1` to open the command plate, select **Remote-SSH: Connect to Host...**, and choose the remote server. I have set ssh configurations, so I can directly see the available remote servers. Done!
- VS Code would remember your action, so next time you open VS Code, you can directly check recent activities to quickly connect ssh.


## TexStudio

I used a Solarized Light theme in [Francis-Hsu's Github](https://github.com/Francis-Hsu/TeXstudio_Solarized). First, I copied the file and save it as `Solarized_Light.txsprofile`, then `Options-> Load Profile` to load it. Note that we need restart TexStudio for the modification to take effects. Another way is to modify the `[format]` section in the setting file `~/.config/texstudio/texstudio.ini`.

# Terminal

## Homebrew
1. Install homebrew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`
2. Install Joplin: `brew cask install joplin`
3. Install Emacs: `brew cask install emacs`
4. Install tmux: `brew install tmux`
5. Install wget: `brew install wget`
6. Install zsh-completions: `brew install zsh-completions`
7. Install zsh-syntax-highlighting: `brew install zsh-syntax-highlighting`
8. Install OpenMP: `brew install libomp`

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
# show the git config info for current git repo
git config user.name
git config --list
```

Secondly, add `id_rsa.pub` to the SSH settings on github website and add shortcuts in `.ssh/config`. Then I shall be able to use git conveniently.

## Emacs

### Configurations
Following the instructions on my previous post [Emacs Configuration](https://yuyangyy.com/blog/posts/Emacs-Configuration/), and remove `elpy, flycheck, ein` packages. 

About Meta keys, since there is something different with my left and right option key between apple keyboard and my HP keyboard. I directly change both option keys to Esc+ in iTerm2 settings. `Profiles -> Keys -> Left(Right) Option Key`.

### Keyboard Shortcuts
References: 
- [Emacs Shortcut Cheatsheet](https://courses.cs.washington.edu/courses/cse351/16wi/sections/1/Cheatsheet-emacs.pdf)
- [Emacs Cheat Sheet by David Cohen](http://www.rgrjr.com/emacs/emacs_cheat.html)

*Add frequently used ones here later.*

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

# solve the conda env issue
# Reference: https://stackoverflow.com/a/62705965/13448382
set -g default-command "/bin/zsh"
```

# Programming 

## RStudio
RStudio would automaticaly detect the required r packages once you open a new R file, so we can easily install the packages all at once with a simple click.

### Good Habits to Keep
1. Create an R project to work with multiple files. In this way, we don't have to set working directory to use data files or refer to other source files.

### Keyboard Shortcuts in RStudio
References:
- [Keyboard Shortcuts from RStudio Support](https://support.rstudio.com/hc/en-us/articles/200711853-Keyboard-Shortcuts)

The following are my frequently used shortcuts.
- `Cmd+Shift+C`: comment and uncomment
- `Ctrl+l`: clear console window
- `Ctrl+1`: switch to source panel
- `Ctrl+2`: switch to console panel

## Python and Conda

### Configurations
#### Anaconda Configurations
I used graphical installer, so I need to initialize conda to add Anaconda to PATH. After refering to the [user guide](https://docs.anaconda.com/anaconda/user-guide/faq/). I did the following to initialize conda.
```bash
source ~/opt/anaconda3/bin/activate
conda init
```

#### Jupyter Configurations
- Set Chrome as the default browser for Jupyter.
    ```bash
    # create jupyter config file if not exists
    # jupyter notebook --generate-config
    # open config file if it exists
    em ~/.jupyter/jupyter_notebook_config.py
    # modify the browser setting
    c.NotebookApp.browser = u'open -a /Applications/Google\ Chrome.app %s'
    ```
- Install extensions
    ```bash
    conda install -c conda-forge jupyter_contrib_nbextensions
    conda install -c conda-forge jupyter_nbextensions_configurator
    ```
### Good Habits to Keep
1. Create a virtual environment and install packages inside it whenever we do a project or just some simple analysis. 

### Conda Environments
References:
- [Managing Environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
I have installed the following virtual environments, each for a specific usage.
```
# create an environment
conda create -n nlp python=3.7
# remove an environment
conda remove --name nlp --all
# check environment info
conda info --envs
```

#### environment.yml
Export `environment.yml` for your conda environment.
```bash
conda activate nlp
conda env export > environment.yml
conda deactivate
```

To create an environment using the `environment.yml` file. The generated environment will have the same name and same packages as the original environment.
```bash
conda env create -f environment.yml
```

#### nlp env
```bash
conda activate nlp
# upgrade pip
pip install -U pip
# install jupyter
pip install notebook
# install pytorch
pip install torch torchvision
# install tensorboard
pip install tensorboard
conda deactivate
```

#### dt env
`dt` is used for data analysis.

```bash
conda create -n dt python=3.7 scipy

conda activate dt
pip install notebook
pip install pandas
pip install lightgbm
pip install xgboost
pip install catboost
pip install shap

conda deactivate
```


# General

## iCloud
Defaultly, when using a new device, iCloud will not download all the files on the cloud to local home directory, instead, it will keep the old versions on the cloud. To download all the files, `System Preferences -> Apple ID`, uncheck `Optimize Mac Storage`.

## Keyboard

### Shortcuts
`Cmd + Space`: I prefer Alfred to Spotlight, so I disabled this shortcut for Spotlight in `Keyboard -> Shortcuts -> Spotlight` and use it in Alfred.

### Key mappings
For MacBook Keyboard
- `Ctrl <-> Caps Lock`: I find it inconvenient to press Ctrl, but it is a frequently used key, so I swapped these two keys.

For my HP keyboard
- `Ctrl <-> Caps Lock`: swap it as well.
- `Option <-> Cmd`: I swap it on the key mappings and on the phisical keyboard.

## Dock
- Check *Automatically hide and show the Dock*.
- Uncheck *Show recent applications in Dock*.
- Put the dock to the left side.