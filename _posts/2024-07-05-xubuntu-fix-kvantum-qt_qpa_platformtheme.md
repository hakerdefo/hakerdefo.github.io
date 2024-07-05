---
layout: post
title: Xubuntu - Fix the QT_QPA_PLATFORMTHEME environment variable is not set correctly error
categories: [how-to, linux]
slug: xubuntu-fix-kvantum-qt_qpa_platformtheme
---

A short while back, I upgraded the minimal installation of Xubuntu Jammy Jellyfish to Noble Numbat, and then I installed Qt5 Configuration Utility (qt5ct) and upon launching, it presented me with the following error,  
> the QT_QPA_PLATFORMTHEME environment variable is not set correctly (current value:gtk2, required value:qt5ct)  

So, I added the following line into the <code>/etc/environment</code> file,  

```bash
export QT_QPA_PLATFORMTHEME=qt5ct
```

Next I performed the logout/login routine and again launched the qt5ct and again the same error persisted to my frustration.  
<!--more-->

A slight digging in the internet dirt made me realize that in the <code>/etc/X11/Xsession.d/56xubuntu-session</code> file, there is a line,  

```bash
export export QT_QPA_PLATFORMTHEME=gtk2
```

And, that very line is the reason for the whole issue. The solution is simple; just change that line above to,  

```bash
export QT_QPA_PLATFORMTHEME=qt5ct
```

And we are done with it. Do the logout/login thing and this time the qt5ct should launch without any errors, and you should be able to theme your QT based applications.  

Adios for now.  

![Qt5 Configuration Utility](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/qt5ct.webp "Qt5 Configuration Utility")
<figcaption>Image courtesy the qt5ct project</figcaption>  
