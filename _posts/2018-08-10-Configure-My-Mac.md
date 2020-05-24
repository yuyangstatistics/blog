---
title: Configure My Mac
date: 2018-08-10 12:28:12 -0500
categories: [System, Configurations]
tags: [mac]
---
New updates are added to the front of this blog.

------------------------------
Update date: Apr. 8
## Emacs
Since several keybindings of Emacs conflict with Mac OSX, I changed some keyboard settings.
`System Preferences -> Keyboard -> Shortcuts -> Input Sources`, I changed the shortcut for "Select the previous input source" to "ctrl + shift + space" to enable using "C-<SPC>" in Emacs.


------------------------------ 
## ssh config and .bash_aliases
Update date: Feb. 19

- Add shortcut to ssh, by modifying `.ssh/config`. For example, I can directly connect to the Lind cluster using `ssh cse-lind`. 
- Create `~/.bash_aliases` file and create short cut in command line. [Reference](https://opensource.com/article/19/7/bash-aliases). Then run `source ~/.bash_profile`.

## Softwares installed

- _**Daily Tools**_
    + Be Focused
    + Wunderlist
    + CheatSheet (show shortcuts)
    + Dr. Unarchiver
    + Clocker (show worldwide time)
    + Spectacle (split screen)
    + Grammarly (check grammar)
    + EuDic
    + Typist

- _**Developing Tools**_
    + Pycharm
    + CLion
    + Anaconda
    + Visual Studio Code
    + Octave (do scentific computation, just like Matlab)
    + R
    + RStudio
    + Python 3.7 (have modified its alias in the **.bash_profile** to be **python3**)
    



## Configurations modified

- Modify the alias of python3.7
```
alias python3="/Library/Frameworks/Python.framework/Versions/3.7/bin/python3.7"
``` 

- Set multiple accounts in Git, by using ssh to connect. Refer details in [Git Notes](https://yuyang-yy.github.io/Git-Notes/).

- Open the firewall of Mac in order to allow **box** to work. (On the **Security & Privacy** part in **System Preferences**)

- Change the port of the *jekyll* blog to 5000, since the previous port 4000 conflicts with *Nomachine* and *box*.


## Configuration in softwares

### Xcode
- Add the terminal shortcut: command + `
    1. write a shell file containing the following two lines, in my case, I save it as *openTerminal.sh*.
    ```
    #!/bin/bash
    open -a Terminal "`pwd`"
    ```
    2. Xcode Preferences -> Behaviors -> User '+' to add a new behavior -> set the shortcuts -> in the right pane *Run*, choose to run *openTerminal.sh*.

- Adjust the font sizes. 
    1. Close all of the projects
    2. Select the items that need font change
    3. Change the font and size. [See details.](https://stackoverflow.com/questions/1339706/how-to-increase-font-size-in-the-xcode-editor)

