---
layout: post
title: Custom Ubuntu install without bloat
categories: [how-to, ubuntu]
slug: custom-ubuntu-install
excerpt: How to install Ubuntu without bloat & turn it into a fast, full-featured desktop with best applications?
---

### Rationale:

There are a zillion flavors of Ubuntu available out there but almost all of them contain things and applications that you don't use & won't ever need, bloat in short. And we all have our personal preferences to handle certain tasks with certain applications. For example you might prefer to play video files via mpv and not VLC. Another good example will be browser, some prefer Chrome over Firefox and some are die hard fans of Vivaldi. If you are a programmer, chances are that you are never gonna use the text-editor that came with the default system install. You might argue that one can install the default Ubuntu and remove unwanted applications later-on. It is only possible in some cases and can be dangerous too. It is highly possible that while uninstalling unwanted applications, automatic dependency resolution will end-up removing whole bunch of required things leaving your system in a broken and unusable state. You get the point?  

### Preparation:

Believe you me it's not that difficult. Even a relatively inexperienced guy can do it and have a full custom desktop system up & running in an hour at max. So ready to go? Great, let's get started then. First thing we'll need is the mini ISO of the latest Ubuntu LTS aka Focal Fossa. It's just 74MB in size. You can download it from here,  
[Ubuntu Focal Fossa mini ISO](http://archive.ubuntu.com/ubuntu/dists/focal/main/installer-amd64/current/legacy-images/netboot/mini.iso){:target="_blank"}  

Now we need to create a boot-able USB drive from the mini ISO we have just downloaded. There are many tools out there to do this but if you are unsure I'd recommend balenaEtcher. Get it from here,  
[Download balenaEtcher](https://www.balena.io/etcher/){:target="_blank"}  

We'll need a partition to install our Ubuntu. If you are not familiar with disk partitioning, I'd advise you to create one with the help of GParted. It's super easy to use and is available for Windows, Linux & Mac OS X. There are tons of videos and tutorials of GParted available on the internet that will help you get started with partitioning using GParted. Get it from here,  
[Download GParted](https://gparted.org/){:target="_blank"}  

Now that we have a partition ready for our custom Ubuntu install, one final thing we need is the magic key that'll let us change the boot order of our computer. This varies from model to model but some common keys are, <code>F10</code>, <code>F11</code>, <code>F12</code>, <code>F2</code>, <code>Delete</code>, <code>Esc</code>, <code>Tab</code>. You can use DuckDuckGo or Google to search for your specific make and model if these keys don't work.  Once we have this information at our hands it's time to restart the computer and boot from our USB.  

### Primary installation:

Rather than repeating or copying/pasting what's already been available, I'd redirect to a wonderful and in-depth guide on installing Ubuntu via mini ISO on Answertopia. This tutorial has images for every installation step that will make it very easy to understand. Follow that guide till the final step <u>1.6 Software Collection Selection</u>. In this step <u>MAKE SURE YOU DON'T SELECT ANYTHING</u>. Just press <code>Continue</code> button without selecting anything there. Here is the link to that guide. Follow it and after the installation finishes and system reboots, come back here and continue with me on this adventure.  
[Installing Ubuntu 20.04 with the Network Installer](https://www.answertopia.com/ubuntu/installing-ubuntu-with-the-network-installer/){:target="_blank"}  

### Secondary installation:

At this point in our journey we are staring at a blank and boring terminal screen after logging in. But worry not we are very near to our goal of a lightweight, fully-featured, bloat-free desktop. First we need to install a few required/must-have stuff for our Ubuntu. Enter the following command to install these things. Press <code>Y</code> key when prompted,  
```text
sudo apt-get --no-install-recommends install lubuntu-desktop lubuntu-update-notifier intel-media-va-driver-non-free intel-microcode libdrm-intel1 xserver-xorg-video-intel amd64-microcode libdrm-amdgpu1 libdrm2 xserver-xorg-video-amdgpu libgl1-mesa-dri mesa-utils mesa-utils-extra mesa-va-drivers mesa-vdpau-drivers mesa-vulkan-drivers ubuntu-drivers-common synaptic xdg-utils apt-xapian-index software-properties-gtk adwaita-icon-theme-full fonts-croscore fonts-crosextra-caladea fonts-crosextra-carlito fonts-noto ffmpeg gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly unzip unrar p7zip-rar xarchiver
```

After the packages are downloaded and installed, enter following commands. Press <code>Y</code> key when prompted,     
```text
sudo apt-get clean
sudo apt-get autoclean
sudo apt-get autoremove
sudo apt-get --no-install-recommends install ttf-mscorefonts-installer
sudo ubuntu-drivers autoinstall
```

Reboot the machine. This time we will be greeted by a lovely LXQT based desktop instead of the boring TTY.  

### Configuration:

Now for some reason systemd starts handling network instead of Network Manager. To fix this problem we need to open terminal and edit a file. To do so enter this in terminal,  
```text
sudo nano /etc/netplan/01-netcfg.yaml
```
A file will open in the nano editor. In this file we need to change this line,  
```text
renderer: networkd
```
to
```text
renderer: NetworkManager
```
Once that is done we can save the file by pressing <code>Ctrl+O</code> keys. That is Press <code>Ctrl</code> button and without releasing it press the <code>O</code> button. Confirm the file saving by hitting the <code>Enter</code> key. Exit the nano editor by pressing <code>Ctrl+X</code> keys. Reboot the machine.  

### Applications:

It's time to install applications. If you are unsure here are a few personal suggestions. But before that some of them will require additional preparation before installation. You can skip any of these steps if you don't want to install that particular application.  
* Google Chrome  
```text
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
sudo apt-get update
sudo apt-get install google-chrome-stable
```

* Vivaldi  
```text
wget -qO- https://repo.vivaldi.com/archive/linux_signing_key.pub | sudo apt-key add -
sudo add-apt-repository 'deb https://repo.vivaldi.com/archive/deb/ stable main'
sudo apt-get update
sudo apt-get install vivaldi-stable
```

* Spotify  
```text
wget -qO https://download.spotify.com/debian/pubkey_0D811D58.gpg | sudo apt-key add -
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
sudo apt-get update
sudo apt-get install spotify-client
```

Here is the applications list. You can use Synaptic or apt-get to install them.  
* Browsers  
  * Firefox (package name = firefox )  
  * Chrome (package name = google-chrome-stable )  
  * Vivaldi (package name = vivaldi-stable )  
* Video players  
  * mpv (package name = mpv )  
  * VLC (package name = vlc )    
  * SMPlayer (package name = smplayer )   
* Audio players  
  * Clementine (package name = clementine )  
  * Audacious (package name = audacious )   
  * Quod Libet (package name = quodlibet )  
* Text editors  
  * Geany (package name = geany )  
  * Notepadqq (package name = notepadqq )  
  * Neovim Qt (package name = neovimqt )  
* Image viewers  
  * photonic (package name = photonic )  
  * Viewnior (package name = viewnior )  
  * nomacs (package name = nomacs )  
* Email clents  
  * Thunderbird (package name = thunderbird )  
  * Claws Mail (package name = claws-mail )  
  * Trojita (package name = trojita )  

Want more apps and more ways to install them? You can use/install <u>snaps</u> via <u>Snap Store</u>. To do so open terminal and run this two commands,  

```text
sudo apt-get --no-install-recommends install snapd
sudo apt-get --no-install-recommends install snap-store
```

Don't forget to keep you customized Ubuntu up-to-date by installing the necessary updates when prompted. You can always update your system manually by running these commands whenever possible (Twice a month is a good choice),  

```text
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### Conclusion:

Now someone might ask why not install Lubuntu instead of going through all this hassle. Well, the answer to will be the same as mentioned at the beginning of this article. Lubuntu for sure is relatively light-weight but it still carries stuff that one might consider bloat, like for example LibreOffice suite. If you are not using word-processors and spreadsheets you will never ever need it. Then there is Discover Software Center, a good looking yet in many ways lacking GUI package manager. Try searching for applications using it and you'll know what I mean. It's definitely inferior to Synaptic in every imaginable way. The applications that come bundled with aren't always the best in their respected categories, say for example Featherpad text-editor or Trojitá email-client. Good but there are way better alternatives out there. Our custom Ubuntu takes around 4.2GB of HDD space and only eats-up about 270MB of RAM. Way lighter than default Lubuntu installation.  

### Customary screenshot:

I'll leave you guys with a screenshot of a working desktop that you'll get after installing Ubuntu using this method.  

![Default Lubuntu Desktop](https://discourse.lubuntu.me/uploads/default/original/1X/16114c085df037446a28b6a7d1f8ef811b0fc73b.jpeg "Example Desktop Screenshot")
<figcaption>Screenshot courtesy team Lubuntu</figcaption>
