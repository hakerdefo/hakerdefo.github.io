---
layout: post
title: How to install NVIDIA drivers in openSUSE
categories: [how-to, linux]
slug: install-nvidia-drivers-opensuse
---

openSUSE doesn’t include proprietary NVIDIA drivers by default. The included Nouveau driver is okay but it is not good enough for gaming and heavy multimedia tasks. openSUSE makes it pretty easy to install the proprietary NVIDIA drivers. Here is a short and to the point guide on installing proprietary NVIDIA drivers in openSUSE.  
<!--more-->

First you need to add the NVIDIA drivers repository. If you are running openSUSE Tumbleweed, run the following command in your favorite terminal emulator,  

```bash
sudo zypper addrepo --refresh https://download.nvidia.com/opensuse/tumbleweed NVIDIA
```

If you are running openSUSE leap, run the following command instead,  
 
```bash
zypper addrepo --refresh https://download.nvidia.com/opensuse/leap/$releasever NVIDIA
```

Next you need to identify the model of your NVIDIA graphics card. To do so, run the following command,  

```bash
sudo hwinfo --gfxcard | grep Model
```

Now that you have identified your graphics card model, it's time to  install the appropriate driver for it.  

For NVIDIA GeForce 700 series and newer cards install the following packages,  

```bash
sudo zypper install x11-video-nvidiaG06 nvidia-glG06
```

For NVIDIA GeForce 600 series cards install the following packages,  

```bash
sudo zypper install x11-video-nvidiaG05 nvidia-glG05
```

For NVIDIA GeForce 400 series cards install the following packages,  

```bash
sudo zypper install x11-video-nvidiaG04 nvidia-glG04
```

For NVIDIA GeForce 8xxx series cards install the following packages,  

```bash
sudo zypper install x11-video-nvidiaG03 nvidia-glG03
```

For NVIDIA GeForce 6xxx series cards install the following packages,  

```bash
sudo zypper install x11-video-nvidiaG02 nvidia-glG02
```

After the driver installation, a system reboot is absolutely essential so, don't forget to restart your computer.  

![NVIDIA GPU](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/gaming-rig.webp "NVIDIA GPU")
