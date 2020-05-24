---
title: Raspberry Pi Installation
date: 2018-07-02 12:28:12 -0500
categories: [System]
tags: [raspberry-pi]
---
Today, my display has finally arrived. I spent two hours on installing the Raspian operating system and coping with the problems about it. The following will illustrate the problems I have met during the process.

I installed Raspberry according to the guidance on the book Raspberry Pi Cookbook.

### Installing steps:
1. Download the NOOBS archive file from [Raspberry official website](http://www.raspberrypi.org/downloads), extract it and place the contents of the file on an SD card. I used the Kingston 32GB TF card and a USB reader.
2. To make the editor more convenient, I use the following commands to install vim editor and configure the **~/.vimrc** file to make vim configuration.
```
sudo apt-get update
sudo apt-get install vim 
```

### Problems I have met:
1. After running the Raspberry Pi, error massages show as: "*Error resizing existing partition. The FAT's don't match....*".
* **Solution**: Although the original tf card is formatted as FAT32, but it may have changed during the process. So I download a [formatting tool](https://www.sdcard.org/downloads/formatter_4/) and then use it to format my SD card, after which I place the NOOBS file contents on the SD card again. 
2. The screen doesn't fill all the display. There are black boarders on the four sides.
* **Solution**: Modify the **/boot/config.txt** file. Note that since this file cannot be overwritten casually, remember to use sudo to write this file. 
3. I tried `scp` command to transfer file between my Mac and the Raspberry Pi, but it turns out to be "*connection refused*".
* **Solution**: The default ssh setting is disabled, so we need to configure ssh first. Pull out the SD card and add a file named "*ssh*" with no postfix to the Root folder. In Mac, use `vim ssh` and then save the file. Then copy this file to the Root folder. After that, the ssh has been enabled and we could use scp command.
