---
title: Linux Notes
date: 2018-08-29 12:28:12 -0500
img: linux.jpg
comments: true
categories: [System]
tags: [linux]
---

1. Common command

    - `top`: shows the resources being used
    - `du -s -h`: shows the storage of the directory
    - `cat /var/log/dmesg | wc -l`: shows the number of lines of a file, a similar example is `w | wc -l`
    - call a variable: use a $
    - export PATH="~/bin:$PATH": search the personal path first, and then the system path.

2. chmod
    - For private files or directory, use `chmod 700 file` to ensure no one else would be able to see.

