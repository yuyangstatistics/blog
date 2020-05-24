---
title: Univ computing
date: 2018-08-29 12:28:12 -0500
img: computing.jpg
comments: true
categories: [Server]
tags: [computing]
---

## Basic Tech 

1. There are two ways to connect to **lts**. (just see the guidance on [Research Computing Resources](http://latis.umn.edu/services-and-programs/research-support/research-planning/additional-research-resources))
    - `ssh x.500@apollo.cla.umn.edu` or `ssh x.500@athena.cla.umn.edu`
    - use Nomachine client to log in

If using ssh, then there would be no graphic display. In such a case, after using `ssh compute` to get into the compute session, `qsub -IX` would not work. Instead, we need to use `qsub -I`, which supports non-graphic option.

Or, I could just use `ssh x.500@compute.cla.umn.edu` to log in **compute**. Do remember `qsub -I` before loading modules and starting to compute.

2. `@c2` means that I am the 2nd in the queue.

3. In order to use **wts**, the software to download is *Microsoft Remote Desktop 8*, not *Microsoft Remote Desktop 10*, since the guidance on the [univ wts](https://cbs.umn.edu/info/internal-resources/faculty-staff/rlt/guides/wts#Mac) is based on version 8. Besides, the vpn should be connected beforehand.

## Parallel Computing

The main instruction of this short course is on [Charles Geyer's website](https://cjgeyer.github.io/Orientation2018/).
