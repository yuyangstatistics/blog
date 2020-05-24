---
title: Reinstall My macOS
date: 2018-07-05 12:28:12 -0500
img: macos.jpg
categories: [System]
tags: [macos]
---

# My experience to reinstall macOS:

I updated the macOS according to the App Store instruction. Nothing strange happened that day, but when I opened my Mac the next day, it kept showing error messages of the newly macOS version. I recorded my experience on Apple website and got feedback call soon. In accordance with the instruction, I did the following steps to recover my computer:

1.  Press `Shift` soon after powering on the Mac and hold this key till the password interface shows up. (In this way, the mac would be in safe-boot mode.)
2.  Backup important data and files using `scp` command, since USB cannot function at safe-boot mode.
3.  Use **App Store** to update system. (If this works, then I don't need to clean the disk to reinstall.)
4.  However, after updating using App Store, it failed again. So I need to clean the disk. Press `Shift + Command + R` soon after powering on and hold these keys till a revolving earth shows up. Then choose the 4th item to clean the Macintosh HD disk and then choose the 2nd item to reinstall system.
5.  Again, error messages about the target disk shows up. According to the instructor's advice, I powered off the computer and implemented the 4th step again(no cleaning procedure this time, just reinsalling system). It works!

# What I have learnt through this experience:

+   Before updating macOS, do remember to backup following:
    +   important data and files
    +   Safari bookmarks
    +   Mac configuration files such as **.bash_profile** and **.vimrc** .
  
# Tasks I have already done:
1. Upgrade my iCloud storage to 50GB. This experience reminds me of the great importance of backing up.

2. Softwares I installed: Wunderlist, Be Focused, Anaconda, Google Chrome, BaiduWangpan, Pycharm, Clion, VSCode, Cheatsheet, Shadowsocks, TexStudio, Texpad, Thunder, MacTex.
    +   To Use **Pycharm** and **Clion**, I need to sign in the Jetbrains website and use my account and password to activate these two softwares.
    +   To use **Texpad**, I need to sign in the TexPad website and use my email and password to activate the softwares.
    +   Installing only the latex platform is not enough, **MacTex** should be downloaded as well. **MacTex** is one of the most popular latex distribution on macOS. 
    +   Unlike the previous macOS version, **Pages**, **Numbers**, and **Keynote** are not installed on this version, so I installed them. 

3. Install homebrew using the code as follows:
> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    While installing homebrew, it shows error message: __*Failed during: git fetch origin master:refs/remotes/origin/master --tags --force*__. After searching Google, I found one [stackoverflow post](https://stackoverflow.com/questions/39836190/homebrew-install-failed-during-git-fetch-origin-masterrefs-remotes-origin-mas). According to its guidance, I run following code, then homebrew is installed successfully.
> git config --global user.email yuyang_96@hotmail.com
>
> git config --global user.name "yuyang"

4. Install Microsoft Office:

    First download the ISO file in the Baiduwangpan, then run the pkg installer file. After installing, just as before, Outlook cannot be used and an error message shows about version being too early. I googled this problem and found [Microsoft Support for macOS High Sierra](https://support.office.com/en-us/article/Microsoft-Office-support-for-macOS-10-13-High-Sierra-80bbd3cc-2412-4593-988a-1c5607b26b28). According to the guidance, I downloaded the latest [Office 2016 for Mac Suite Installer](https://go.microsoft.com/fwlink/?linkid=525133). Maybe next time, I don't need to download file in Baiduwangpan, but just the file in the link above.

5. When I configured jekyll to set up my blog according to the guidance on [Kresnik's Blog](http://kresnik.wang/works/tech/2015/06/07/在github-pages网站下用jekyll制作博客教程.html), after implementing 
> gem install jekyll

    I ran 
> jekyll -v

    Error messages showed up: __*Could not find gem 'jekyll-sitemap' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)*__. After googling it, I find one [jekyll Github issue](https://github.com/jekyll/jekyll/issues/4972) illusrating this problem. I then ran the following code:
> gem install jekyll-sitemap
> 
> gem install pygments.rb
> 
> gem install jekyll-paginate
> 
> gem install jemoji
> 
> gem install bundler
> 
> bundle install

    When I open Gemfile, *jekyll-sitemap*, *jekyll-paginate*, *jemoji* are in the file. According to the output of bundle install, I add `source 'https://rubygems.org'` to the Gemfile. Then, jekyll performs normally. The key to solve the problem, I suppose, is to install all the file in the Gemfile first.

6. I configured terminal based on the guidance on [Udacity's course on Git](https://classroom.udacity.com/courses/ud775/lessons/2980038599/concepts/33331589510923), using __*git-completion.bash*__ and __*git-promp.sh*__.

7. Jupyter notebook:

    Since jupyter notebook has already been installed on Anaconda, I can use the following code on terminal to start jupyter notebook. 
> /anaconda3/bin/jupyter-notebook

    Or, I could just run:
> jupyter notebook


8. Set autostarting softwares:

    System Preferences -> Users & Groups -> unlock to make changes -> add **ShadowsocksX-NG-R8** and **Be Focused**.

9. Disable Guest User login:

    System Prefereneces -> Users & Groups -> unlock to make changes -> turn off guest user option

10. Configure terminal:

    Terminal Preferences -> Profiles -> Text and Window option

11. Check java and jdk:

    This mac doesn't have java, so I downloaded and installed them. I used 8u171 version.

12. Enable starting VSCode through terminal command:`code`:

    * Open VSCode, Shift + Command + P
    * input `shell`
    * Choose to __install code command in PATH__.

13. Set the mac to turn display off after 1 hour. 

14. Disable macOS automatically updates notification in App Store Preferences.

15. Set the outside keyboard.
    - System Preferences -> keyboard
    - choose the external keyboard and choose to modify keys
    - exchange the **option** and **command**.

16. Install Xcode, Dropbox, Google Drive, NoMachine(for **lts**), Box Sync, Cisco(for **vpn**), Mircosoft Remote Desktop(for **wts**), Fugu, Canon IJ Scan Utility Lite(for **printer**), Be Focused Pro, Evernote, Zotero, Praat(for **GRAD 5105**).

