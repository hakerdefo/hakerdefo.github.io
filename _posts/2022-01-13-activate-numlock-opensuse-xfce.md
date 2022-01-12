---
layout: post
title: How to activate numlock on by default in openSUSE with Xfce
categories: [how-to, numlock]
slug: activate-numlock-opensuse-xfce
---

## Problem:

You have openSUSE with Xfce desktop environment installed and you want to turn numlock on by default so that you can use the number-pad on your keyboard at the login screen and after logging-in to Xfce desktop. This should have been the default behavior but sadly it's not! Anyway, it's an easy problem to fix. This solution is written for openSUSE but it should work on almost all GNU/Linux distributions with Xfce desktop environment and LightDM display manager.  
<!--more-->

## Solution:

First and foremost, you need to install a little utility called <code>numlockx</code>. To do so, open your terminal emulator and run the following command,  
```bash
sudo zypper install numlockx
```
Next, create a blank file with the name <code>60-numlock.conf</code>in the <code>/usr/share/lightdm/lightdm.conf.d</code> directory. To do so, run this command in the terminal emulator,  
```bash
sudo touch /usr/share/lightdm/lightdm.conf.d/60-numlock.conf
```
Now open this file as root or with sudo permissions in your favorite text-editor and paste the following code snippet into the file and save the changes,  
```bash
[Seat:*]
greeter-setup-script=/usr/bin/numlockx on
```
Final step is to make a tiny change in the <code>Keyboard</code> settings. You can navigate to this settings window like this,  
```bash
Menu => Settings => Keyboard
```
And in the <code>Keyboard</code> settings window you'll find <code>Restore num lock state on startup</code> option in the <code>General/code> section under the <code>Behavior</code> tab. Enable this by clicking on the check mark box.  

That's it! This will keep numlock on by default all the way from logging screen and onto the Xfce desktop session.  
