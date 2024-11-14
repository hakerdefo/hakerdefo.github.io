---
layout: post
title: ALT Linux - How to replace PulseAudio with PipeWire
categories: [how-to, linux]
slug: replace-pulseaudio-with-pipewire
---

ALT Linux uses PulseAudio as its default sound server but, switching to PipeWire is not that difficult. ALT Linux English wiki doesn't have any documentation on this subject as of writing this article, so I decided to post this little how-to with the hope that someone will find it useful.  
<!--more-->

First we need to install PipeWire and a few useful helper tools. It's as easy as running the following in the terminal emulator of your choice,  

```bash
sudo apt-get install pipewire pipewire-utils wireplumber easyeffects
```

Next, it's time to disable PulseAudio related services. Run the following commands as regular user, I repeat, as a regular user and not as root or with sudo.  

```bash
systemctl --user disable --now pulseaudio{,.socket,-x11}
systemctl --user mask pulseaudio{,.socket,-x11}
```

Finally, it's time to enable PipeWire related services & WirePlumber,  

```bash
systemctl --user enable --now pipewire{,-pulse}{,.socket} wireplumber
```

A logout/login should be good enough, but if possible a reboot is highly recommended.  

To verify that whether PipeWire is up & running, run the following command,  

```bash
pactl info | grep 'Server Name' | cut -d " " -f 3-
```

If everything is working as it should, the term **PipeWire** should appear in the output, followed by the version number. Something like the following,  

```bash
PulseAudio (on PipeWire 1.2.6)
```

Voilà! We have successfully switched to PipeWire as the default sound server. And, oh by the way, don't forget to play around with **EasyEffects**.  

![The word Audio written on a neon sign](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/audio.webp "The word Audio written on a neon sign") 
<figcaption>Image courtesy Thomas Hawk</figcaption>  
