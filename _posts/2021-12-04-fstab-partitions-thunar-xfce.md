---
layout: post
title: How to fix fstab partition entries not showing up in Thunar in XFCE
categories: [how-to, fstab]
slug: fstab-partitions-thunar-xfce
---

## Problem:

You want to mount certain partitions at custom mount points with specific file system options so you define all that in <code>/etc/fstab</code> file but after doing so you discover that Thunar file manager of XFCE doesn't show those partitions! What's wrong? How to make Thunar display those partitions?  
<!--more-->

## Solution:

Well, as it turns out the solution to this problem is really simple. All you need to do is add <code>comment=x-gvfs-show</code> option to your partition entries in <code>/etc/fstab</code> file. For example let's say you added an fstab entry for your partition <code>sda1</code> like this,  
```bash
/dev/sda1	/mnt/sda1	ext4	defaults,noauto,noatime	0	0
``` 
And it didn't show up in Thunar. All you need to do now is add <code>comment=x-gvfs-show</code> option to this entry like this,  
```bash
/dev/sda1	/mnt/sda1	ext4	defaults,noauto,noatime,comment=x-gvfs-show	0	0
```
Save the file once you are done editing and reboot your computer. Rebooting is not strictly necessary as a log-out and log-back-in routine is good enough for most cases. Start Thunar and it'll definitely show those partitions entries now. If it is not, then I'm afraid you'll have to wield your hammer!  
