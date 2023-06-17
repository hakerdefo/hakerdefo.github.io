---
layout: post
title: How to install Brave & Vivaldi browsers in openSUSE
categories: [how-to, linux]
slug: install-brave-vivaldi-browsers-opensuse
---

I'm an avid Firefox user and it has been the browser for me for the ages but due to a recent [Firefox bug in openSUSE Tumbleweed](https://bugzilla.opensuse.org/show_bug.cgi?id=1212101){:target="_blank"}, I was in need for a temporary browser alternative. I shortlisted Brave and Vivaldi as decent Firefox placeholders. Sadly, Brave and Vivaldi are not available in the official repositories of openSUSE but installing them is a relatively straightforward and easy process,  
<!--more-->

### Installing Brave on openSUSE  

This can be done in a few different ways but here is how I did it,  
Create a new file with the name <code>brave-suse.repo</code> in the <code>/etc/zypp/repos.d/</code> directory,  

```bash
sudo touch /etc/zypp/repos.d/brave-suse.repo
```

Next, copy-paste the following text snippet into the <code>/etc/zypp/repos.d/brave-suse.repo</code> file,  

```bash
[brave-browser]
name=brave-browser
enabled=1
autorefresh=1
baseurl=https://brave-browser-rpm-release.s3.brave.com/$basearch
type=rpm-md
gpgcheck=1
keeppackages=0
```

Save the changes made to the file.  
Open your favorite terminal emulator and import Brave browser's repository signing keys,  

```bash
sudo rpm --import https://brave-browser-rpm-release.s3.brave.com/brave-core.asc
```

And, install Brave browser,  

```
sudo zypper refresh
sudo zypper install brave-browser
```

### Installing Vivaldi on openSUSE  

The process of installing Vivaldi browser is going to be very similar to the Brave install process above.  
Create a new file with the name <code>vivaldi-suse.repo</code> in the <code>/etc/zypp/repos.d/</code> directory,  

```bash
sudo touch /etc/zypp/repos.d/vivaldi-suse.repo
```

Add the following text snippet into the <code>/etc/zypp/repos.d/vivaldi-suse.repo</code> file,  

```bash
[vivaldi]
name=vivaldi
enabled=1
autorefresh=1
baseurl=https://repo.vivaldi.com/archive/rpm/$basearch
type=rpm-md
keeppackages=0
gpgcheck=1
gpgkey=https://repo.vivaldi.com/archive/linux_signing_key.pub
```

Save the file.  
Open a terminal emulator and run the following commands to install Vivaldi browser,  

```
sudo zypper --gpg-auto-import-keys refresh
sudo zypper install vivaldi-stable
```

![Internet sign on a pole](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/internet_pole_roof_tiles.jpg "Internet sign on a pole")  
<figcaption>Image courtesy Anna Carol</figcaption>  
