---
title: Cluster Notes
date: 2020-02-19 12:28:12 -0500
categories: [Server, CSElabs]
tags: [server]
---

# MSI
1. [Jupyter Notebook](https://www.msi.umn.edu/support/faq/how-do-i-get-started-jupyter-notebooks)
2. [FileZilla](https://www.msi.umn.edu/support/faq/how-do-i-use-filezilla-transfer-data) to transfer data files.
3. [Cuda](https://www.msi.umn.edu/sw/cuda) and [GPU number setting](https://github.com/allenai/allennlp/issues/1090)

Use the same configuration as in CSE Labs, configure ssh to login without password.


## Question to ask MSI staff
1. How to configure the environment for Jupyter notebook? Can I start Jupyter notebook in one environment?

# CSE Labs

1. Set ssh to login without password. Do this on the local machine. Run the following step by step exactly. Check the [reference](http://www.linuxproblem.org/art_9.html) for more detail.
    - Don't change `id_rsa` to other names. Don't enter passphrase. Just press Enter for three times. 
        ```
        ssh-keygen -t rsa
        ```
    - Even if there are .ssh in the cluster, run it.
        ```    
        ssh x500@csecluster mkdir -p .ssh
        ```
    - 
        ```
        cat .ssh/id_rsa.pub | ssh x500@csecluster 'cat >> .ssh/authorized_keys'
        ```
    - Now I can log in without a password.
        ```
        ssh x500@csecluster
        ```
2. Set ssh to switch among the clusters without a password. Do this on the cluster machine.
    - Login to one cluster first.
    - Run the following code inside the cluster.
        ```
        ssh-keygen -t rsa -P ""
        cat ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys
        ```
3. Set ssh aliases. Do this on the local machine. Check the [reference](https://www.ostechnix.com/how-to-create-ssh-alias-in-linux/) for more detail.
    - Edit the `~/.ssh/config` file. Can also do for phixx and cudaxx account.
        ```
        # CSElabs Lind account
        Host cse-lind
            HostName CSEcluster
            User x500
            IdentityFile ~/.ssh/id_rsa
            UseKeychain yes
        ```
    - Then we can directly connect to the cluster using the following.
        ```
        ssh cse-lind
        ```
4. Set ssh aliases among the terminals. Do this on the cluster machine. 
    - Create and edit the `~/.ssh/config` file.
        ```
        Host phi01
            HostName phi01.cselabs.umn.edu
            User yang6367
            IdentityFile ~/.ssh/id_rsa
        ```
    - Then we can switch among the clusters. For example, inside the lind machine, switch to phi01 machine.
        ```
        ssh phi01
        ```
5. Modify the prompt format. Copy [git-completion.bash](https://raw.githubusercontent.com/yuyang-yy/materials/master/config/terminal/git-completion.bash) and [git-prompt.sh](https://raw.githubusercontent.com/yuyang-yy/materials/master/config/terminal/git-prompt.sh) files to the cluster machine. Then add the following to the `.bashrc` file.
    ```
    # Enable tab completion
    source ~/git-completion.bash

    # colors!
    green="\[\033[0;32m\]"
    blue="\[\033[0;34m\]"
    purple="\[\033[0;35m\]"
    reset="\[\033[0m\]"

    # Change command prompt
    source ~/git-prompt.sh
    export GIT_PS1_SHOWDIRTYSTATE=1
    # '\u' adds the name of the current user to the prompt
    # '\$(__git_ps1)' adds git-related stuff
    # '\W' adds the name of the current directory
    export PS1="$purple\u@$green\h\$(__git_ps1)$blue \W $ $reset"
    ```
6. My modules are obsolete, and could not load `hpc/openmpi` module. After asking Prof. Saad for help, I got the solution. Edit `~/.bashrc` file. Change the `MODULESINIT` as the following.
    ```
    MODULESINIT="/soft/rko-modules/tcl/init/bash"
    ```
