---
layout: post
title: How to activate numlock on by default in Manjaro or any other Arch derivative
categories: [how-to, numlock]
slug: activate-numlock-manjaro-arch-xfce
---

## Problem:

You have Manjaro with Xfce desktop environment installed and you want to turn numlock on by default so that you can use the number-pad on your keyboard at the login screen and after logging-in to Xfce desktop. This should have been the default behavior but sadly it's not! Anyway, it's an easy problem to fix. This solution is written for Manjaro but it should work on almost all Arch Linux based distributions and derivatives with LightDM display manager.  
<!--more-->

## Solution:

First and foremost, you need to install a little utility called <code>numlockx</code>. To do so, open your terminal emulator and run the following command,  
```bash
sudo pacman -S numlockx
```
Next, open the file <code>/etc/lightdm/lightdm.conf</code> in your favorite text-editor. For example you can use <code>GNU nano</code> to do so,  
```bash
sudo nano /etc/lightdm/lightdm.conf
```
And in that file under the <code>[Seat:*]</code> section, you'll find the following line,  
```bash
#greeter-setup-script=
```
Uncomment that line and add the path to <code>numlockx</code> and a command switch to toggle it on like this,  
```bash
greeter-setup-script=/usr/bin/numlockx on
```
Save the changes to the file. If you are using Xfce desktop environment, one final step you'll have to take is to make a tiny change in the <code>Keyboard</code> settings. You can navigate to this settings window like this,  
```bash
Menu => Settings => Keyboard
```
And in the <code>Keyboard</code> settings window you'll find <code>Restore num lock state on startup</code> option in the <code>General</code> section under the <code>Behavior</code> tab. Enable this by clicking on the check mark box.  
That's it! This will keep numlock on by default the next time you boot your system. You'll have numlock on all the way from logging screen and onto the desktop session.  
