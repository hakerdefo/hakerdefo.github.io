---
layout: post
title: How to fix LightDM GTK+ Greeter Settings editor GUI not opening issue
categories: [how-to, lightdm]
slug: fix-lightdm-editor-gui
excerpt: You want to customize LightDM Greeter but the settings editor GUI for LightDM GTK+ Greeter won't open after you have entered your password in the prompt dialogue. You are sure that every dependency is satisfied and you are not entering the wrong password. What could be wrong here and how to fix this issue?
---

## Problem:

You want to customize **LightDM Greeter** but the settings editor GUI for **LightDM GTK+ Greeter** won't open after you have entered your password in the prompt dialogue. You are sure that every dependency is satisfied and you are not entering the wrong password. What could be wrong here and how to fix this issue?  

## Solution:

I faced this very issue during my migration from **openSUSE Leap** to **openSUSE Tumbleweed**. I installed **Tumbleweed** with **XFCE** desktop environment and when I tried to launch the **LightDM GTK+ Greeter Settings editor GUI** from the **XFCE Settings Manager**, I discovered that it would prompt me to enter my superuser password but it wouldn't launch after that. After quite a bit of digging around I solved the issue and the culprit in this case turned out to be missing aka empty **hostname**. The solution is pretty straightforward. Open your favorite **terminal emulator** and run the following command replacing the <code>new.host.name</code> in the command with your desired **hostname**,  
```bash
sudo hostnamectl set-hostname new.host.name
``` 
It is not required but I would suggest you to reboot the system and once the system is back up and running, try launching the **LightDM GTK+ Greeter Settings editor GUI** with your fingers crossed! This solved my issue and it might solve yours too!  
Go try this!  
