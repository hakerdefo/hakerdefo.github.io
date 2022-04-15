---
layout: post
title: An alternative method to upgrade to Ubuntu 22.04 LTS (Jammy Jellyfish)
categories: [how-to, linux]
slug: upgrade-ubuntu-to-jammy-jellyfish
---

I recently upgraded my installation of Ubuntu 20.04 LTS (Focal Fossa) to Ubuntu 22.04 LTS (Jammy Jellyfish). Ubuntu comes with a bundled tool to handle the upgrade process, but I decided to do it a bit differently. This method is a bit more manual compared to the default Ubuntu method but, in my view, it gives more transparency and more control over the upgrade process. Here is how one can upgrade from Ubuntu 20.04 LTS (Focal Fossa) to Ubuntu 22.04 LTS (Jammy Jellyfish),  
<!--more-->

First we need to make sure that our current install is up-to-date and no package or dependency is missing or corrupt. Open your favorite terminal-emulator and run the following commands in the exact order,  

```bash
sudo apt-get update
sudo apt-get --fix-broken install
sudo apt-get dist-upgrade
sudo apt-get clean
sudo apt-get autoclean
sudo apt-get autoremove
```

Now, it's time to start the actual upgrade process. First, we need to rename the current **sources.list** file and create a new **sources.list** file for Ubuntu 22.04 LTS (Jammy Jellyfish). To do so, run these commands,  

```bash
sudo mv /etc/apt/sources.list /etc/apt/sources.list.bak
sudo touch /etc/apt/sources.list
```

Open the newly created <code>/etc/apt/sources.list</code> file with sudo or root privileges in a text-editor of your choice and paste the following snippet into it and save the file,  

```bash
deb https://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse
# deb-src https://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse

deb https://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse
# deb-src https://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse

deb https://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
# deb-src https://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse

deb https://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse
# deb-src https://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse

deb http://archive.canonical.com/ubuntu jammy partner
# deb-src http://archive.canonical.com/ubuntu jammy partner
```

Log out of your current session and press <code>Ctrl</code>+<code>Alt</code>+<code>F2</code> keys together to switch to **tty2** and log in to your user account there and let the upgrade rollercoaster begin by running these commands,  

```bash
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get clean
sudo apt-get autoclean
sudo apt-get autoremove
```

When the upgrade process completes, restart your computer,  

```bash
sudo shutdown -r now
```

If nothing went south during the above process, you should be able to boot into your shiny-new Ubuntu 22.04 LTS (Jammy Jellyfish) now.  

Ubuntu 22.04 LTS (Jammy Jellyfish) ships with a **Snap** package of Mozilla Firefox instead of traditional **Deb** package. During my upgrade process, the updater failed to connect to the **Snap Store** and presented me with three choices; **Retry**, **Skip** or **Abort** the upgrade. I selected the **Retry** option several times, but the same error prevailed, so I went with the **Skip** option and after the upgrade process completed, I rebooted the machine and manually installed the Mozilla Firefox,  

```bash
sudo apt-get --no-install-recommends install firefox
``` 

The above command will install Firefox. Be aware that the above command might take some time to complete, and it's not really a verbose process, so enjoy a cup of tea or coffee while it completes.  

![Ubuntu Jammy Jellyfish")](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/jammy_jellyfish.webp "Ubuntu Jammy Jellyfish")
<figcaption>Image courtesy Hsingchien Cheng</figcaption>  
