---
layout: post
title: How to install multimedia codecs in openSUSE
categories: [how-to, linux]
slug: install-multimedia-codecs-opensuse
---

openSUSE doesn’t include proprietary and patented software by default. Many codecs required to decode and play some common and popular multimedia formats, hence aren’t available, and those multimedia files can’t be played. A third party repository, called Packman, provides these missing codecs for openSUSE. Adding the Packman repository and installing all the necessary multimedia codecs is a relatively straightforward task. Here is how you can do it,   

Open your favorite terminal emulator and run the following commands in the given order,  

```bash
sudo zypper ar -cfp 90 https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Tumbleweed/Essentials packman-essentials  
sudo zypper refresh  
sudo zypper dup --from packman-essentials --allow-vendor-change  
sudo zypper install ffmpeg libavcodec-full vlc-codecs pipewire-aptx gstreamer-plugins-bad-codecs gstreamer-plugins-ugly-codecs gstreamer-plugins-libav gstreamer-plugins-good gstreamer-plugins-good-extra gstreamer-plugins-bad gstreamer-plugins-ugly  
```

If you are running openSUSE Leap instead of openSUSE Tumbleweed, replace the very first command above with this one,  

```bash
sudo zypper ar -cfp 90 https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Leap_$releasever/Essentials packman-essentials  
```

The rest of the commands will remain the same as the above.  

![openSUSE](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/opensuse.webp "openSUSE")  
