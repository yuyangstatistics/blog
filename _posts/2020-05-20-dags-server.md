---
title: Dags Server
date: 2020-05-20 12:22:12 -0500
categories: [Server, Linux]
tags: [server]
---
## Load modules
In order to use Jupyter notebook and python3.7, I need to load module `python/conda/3.7` first.

To automatically load specific software module or modules every time you log into the server, edit your `.bashrc` file:

```bash
> module load python/conda/3.7
```

## Virtual Environments
Keep a habit of using virtual environments, especially in a remote server where I am not the root. One biggest different between local machines and remote machines is that you won't have the permission to install packages as you want, and you are only allowed to install packages on your local directory. If you want to install a python package for general purposes, use `pip install --user packagename`. But usually, we work on projects and should set different environments for different projects, so creating a conda virtual environment and install packages inside would be a better idea.

```bash
> module load python/conda/3.7
> conda create -n envname python=3.7
> conda activate envname
> conda install packages
> conda deactivate
```

Note: in order to use `conda activate`, we need to run `conda init bash` to initialize conda commands.

Now you can install packages you would like to use, without worring about not having root permissions.

To see the information of the environments, run:

```bash
> conda info --envs
```

## Jupyter notebook

References:
- [Running a Jupyter notebook from a remote server](https://ljvmiranda921.github.io/notebook/2018/01/31/running-a-jupyter-notebook/)
- [How do I remove an SSH forwarded port](https://superuser.com/questions/87014/how-do-i-remove-an-ssh-forwarded-port)

If you have created a conda virtual environment as before and have activated it, then jupyter notebook is defaultly installed. There are several steps.

1. In the remote host, run:

```bash
> jupyter notebook --no-browser --port=8889
```

2. In the local computer, run:

```bash
> ssh -N -f -L localhost:8888:localhost:8889 x500@dags
```

Note: I have configured dags in my ssh configuration, so I just use the shortcut of the host name.

3. Open local browser and type **localhost:8888**.

### Use functions to simplify
Use functions or aliases to make the above steps easier. The reference used functions and for simplicity, I aliases.

1. In the remote host, add the function below to `.bashrc`.

```
function jpt(){
	jupyter notebook --no-browser --port=$1
}
```

2. In the local host, add the function below to `.zshrc`. (I am using zsh in my local computer.)

```
function jptt(){
	ssh -N -f -L localhost:"$2":localhost:"$1" x500@dags
}
```
Note: for zsh, do remember to add single quote or double quote.

3. Then every time you want to run jupyter notebook, just do:

remotely, 

```bash
> jpt 8889
```

locally, 

```bash
> jptt 8889 8888
```

Open browser and type **localhost:8888**. Done!

### Use aliases to simply
For simplicity, I set the default remote port to be 8889, and the default local port to be 8888. Feel free to change it.

1. Edit `.bash_aliases` in the remote server.

```bash
alias jpdags="jupyter notebook --no-browser --port=8889"
```

2. Edit `.zshrc` in the local machine.

```bash
# establish ssh tunnel and use Chrome to open the link
alias jpdags="ssh -N -f -L localhost:8880:localhost:8889 x500@dags; open -a 'Google Chrome' 'http://localhost:8880/tree?'"

# kill related ssh processes
alias kjpdags="lsof -i:8880"  # this one gives a cleaner output, it shows the PID related to local port 8880
# alias kjpdags="ps aux | grep '8889.*dags'"
```

Now, the browser window will automatically open.

Note: remember to add single quote around the url link and the regular expression in grep.

3. Close jupyter in the remote server using 'Ctrl + c'.

4. Kill relevant ssh processes by running `kjpdags` and `kill <PID>` with PID shown in the grep results.


## Install Packages

Keep in mind that all of these packages should be installed in a virtual environment.

### PyTorch
First, check the available cuda modules and the GPU information. In dags server, the newest version of cuda is 10.0.130, and the cuda version for the GPUs is 10.2. Which version should I use then? 10.2 means the GPU can deal with at most 10.2 version of cuda, so it is fine to have lower versions. In the official pytorch website, the available cuda versions for 1.5.0 are 9.2, 10.1, and 10.2. I tried all of them using conda, and none of them works. I then tried pip under the version 10.1, and it worked!

```bash
> module avail
> nvcc -V

> nvidia-smi
```

```bash
> pip install torch==1.5.0+cu101 torchvision==0.6.0+cu101 -f https://download.pytorch.org/whl/torch_stable.html
```

Or, we don't need to consider the cuda version at all. Directly specifying `torch` in the `environment.yml` works as well.

### Tensorboard
Note that don't install tb-nightly, just tensorboard. And the following steps should be done in the virtual environment.

In order to use tensorboard in remote servers, similar to jupyter notebook, we would need to use ssh tunnels. The complete steps are as follows.

1. Write summary to a logdir. When logdir is not specified, the default is `./runs`. Note that the path here is relative path, so it is important to change directory to the path of this snippet of code of jupyter notebook to use tensorboard.
	```python
	from torch.utils.tensorboard import SummaryWriter

	# logdir: runs
	writer = SummaryWriter()  
	r = 5
	for i in range(100):
		writer.add_scalars('run_14h', {'xsinx':i*np.sin(i/r), \
			'xcosx':i*np.cos(i/r), 'tanx': np.tan(i/r)}, i)
	writer.close()

	# logdir: my_experiment
	writer = SummaryWriter("my_experiment") 
	for i in range(10):
		x = np.random.random(1000)
		writer.add_histogram('distribution centers', x + i, i)
	writer.close()
	```

2. Open a new tmux window, activate the corresponding conda virtual environment, change directory to the path of the code or jupyter notebook. You should find the logdir there. Then run the following in shell. We may skip the port option, since the default port for tensorboard is 6006.
	(1) if use the default logdir.
 	```bash
	tensorboard --logdir=runs --port=6006
	```
	(2) if use self-defined logdir, for example, my_experiment.
	```bash
	tensorboard --logdir=my_experiment --port=6006
	```

3. Build ssh tunnel to open tensorboard locally.
	```bash
	ssh -N -f -L localhost:16006:localhost:6006 x500@dags
	```

4. Then we should be able to open `localhost:16006` and see the results.

5. After finishing, do remember to end the tensorboard and kill the tunnels. To kill the tunnels, run the following.
	```bash
	lsof -i:6006

	kill -9 PID
	```

#### Simplify the procedure
Similar to what we have done in jupyter notebook, we can set aliases to simplify the whole procedure. We use the default port 6006.

Remotely, add the following function to `.bashrc`.
```bash
function tb(){
	tensorboard --logdir=$1
}
```

Locally, add the following to `.zshrc`
```bash
alias tbdags="ssh -N -f -L localhost:16006:localhost:6006 x500@dags; open -a 'Google Chrome' 'http://localhost:16006'"
alias ktbdags="lsof -i:16006"
```

Then what you need to do is
1. Remotely, write summary, change directory to the code path, then run `tb [logdir]`.
2. Locally, run `tbdags`. After finishing, run `ktbdags` and `kill -9 <PID>`.

## Helpful Tools

### Remote Development using VS Code

References
- [Remote Development using SSH](https://code.visualstudio.com/docs/remote/ssh)

Install the Remote Development extension pack in VS Code, and this would enable us to use VS Code to edit remote files.

- Open VS Code, press `F1` to open the command plate, select **Remote-SSH: Connect to Host...**, and choose the remote server. I have set ssh configurations, so I can directly see the available remote servers. Done!
- VS Code would remember your action, so next time you open VS Code, you can directly check recent activities to quickly connect ssh.

### TMUX
Check [Tmux Cheat Sheet & Quick Reference](https://tmuxcheatsheet.com) to refresh your memory about hot keys. It would be very helpful if you can memorize them.

There are three levels in tmux: sessions, windows, and panes. Usually, we would create a session for a new project, a window for a new task, and a pane for convenient reference when writing code. For example, if I am working on NMT, then I would create a session named `nmt`. Inside this session, I would create a window `jupyter` to open jupyter notebook, `tensorboard` to open tensorboard, `bash` to do the others.

There are several commands that I feel important and used often.

`-t`: target
`-a`: all but

#### session
- create
	- unnamed: `tmux`
	- named: `tmux new -s [name]`
- kill
	- current: `tmux kill-session`
	- named: `tmux kill-session -t [name]`
	- all but current: `tmux kill-session -a`
	- all but named: `tmux kill-session -a -t [name]`
	- all: `tmux kill-server`
- rename: `Ctrl+b+$`
- detach *(jump out of tmux)*: `Ctrl+b+d`
- attach *(go back into tmux)*
	- attach the last: `tmux a`
	- attach named: `tmux a -t [name]`
- move to the next/previous: `Ctrl+b+(` / `Ctrl+b+)`
- get tmux session info: `Ctrl+b+s` / `tmux ls`

#### window
- create: `Ctrl+b+c`
- rename: `Ctrl+b+,`
- close: `Ctrl+b+&`
- move to the next/previous: `Ctrl+b+n` / `Ctrl+b+p`
- select a specific window: `Ctrl+b+[0-9]`
- swap windows: `tmux swap-window -s [source] -t [target]`

#### pane
- create
	- split vertically: `Ctrl+b+%`
	- split horizontally: `Ctrl+b+"`
- close: `Ctrl+b+x`
- switch among panes
	- by arrow: `Ctrl+b+[arrow_key]`
	- by number: `Ctrl+b+q+[0-9]`
	- to the next pane: `Ctrl+b+o`
- show pane number: `Ctrl+b+q`

## Other Configurations

### aliases
- I uncommented `unalias rm` in the `.bash_aliases` file, since the rm questions are disturbing.

### SSH
References:
- [client_loop: send disconnect: Broken pipe](https://www.nixcraft.com/t/client-loop-send-disconnect-broken-pipe/2708/4)

I came across the error message `client_loop: send disconnect: Broken pipe` many times, and it turns out it has to do with inactive connection. Three options are related to keeping connection alive: `TcpKeepAlive`, `ServerAliveInterval`, `ServerAliveCountMax`. So I modify the ssh configuation file a bit, as follows. Now, my client will sent "keep-alive" message to the server every 60 seconds, and after 60 counts without response, the connection will consider it as inactive and break the pipe.

```bash
Host dags
     HostName xxx
     User xxx
     IdentityFile xxx
     UseKeychain yes
     TcpKeepAlive yes
     ServerAliveInterval 60
     ServerAliveCountMax 60
```