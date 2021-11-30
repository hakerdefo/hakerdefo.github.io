---
layout: post
title: How to fix Grub2 install error
categories: [how-to, grub2]
slug: fix-grub2-install-error
excerpt: You want to install Grub2 bootloader onto a partition on your system's hard-disk but the installation is failing with an error message complaining about something called blocklists and you are 100% clueless about this blocklists thing and don't know how to fix this issue. Well, worry not! It only takes a singe flag to fix this error!
---

## Problem:

You want to install Grub2 bootloader onto a partition on your system's hard-disk but the installation is failing with an error message saying,  
> grub-install: error: will not proceed with blocklists.

You are clueless about this particular error and don't know how to fix this issue. Well, worry not! It only takes a singe flag to fix this error! Really, you only have to append a single flag to the Grub2 install command to solve this.  

## Solution:

Let's for example say, you want to install Grub2 onto <code>sda1</code> partition of your hard-disk and you run the following command to do so,  
```bash
sudo grub-install /dev/sda1
```
But for some unknown reasons the installation fails with the error,  
```bash
Installing for i386-pc platform.
grub-install: warning: File system `ext2' doesn't support embedding.
grub-install: warning: Embedding is not possible.  GRUB can only be installed in this setup by using blocklists.  However, blocklists are UNRELIABLE and their use is discouraged..
grub-install: error: will not proceed with blocklists
```
Well, solution for this problem is very very simple. You only have to append the <code>--force</code> flag to that command. So the above command will need a slight modification like this,  
```bash
sudo grub-install --force /dev/sda1
```
And this should hopefully install Grub2 onto the <code>sda1</code> partition.  

Happy booting!  

