---
layout: post
title: How to assign persistent network interface names on Debian 
categories: [how-to, linux]
slug: persistent-network-interfaces-names-debian
---

## Problem:

You have configured the network in your Debian install via the <code>/etc/network/interfaces</code> file and everything seems to work, except the name of your configured network interface keeps changing after every reboot and that is resulting in the network being down. How do you assign persistent network interface names to fix this issue?  
<!--more-->

## Solution:

Let's assume that you are configuring an interface named <code>eth0</code>. We need to get the MAC address of this interface. To do so, open terminal emulator and run the following command,  

```bash
ip link show
```

The above command will list all interfaces names and their MAC addresses. Note down the MAC address of the interface that you wish to rename. Let's assume that the MAC address is <code>b4:96:91:14:ae:5a</code>.  

Now we need to modify the <code>/etc/network/interfaces</code> file slightly. Your <code>/etc/network/interfaces</code> file currently should look something like this,     

```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback
#
# The primary network interface
allow-hotplug eth0
iface eth0 inet dhcp
#
# This is an autoconfigured IPv6 interface
iface eth0 inet6 auto

```

In the above file, we need to change <code>eth0</code> to something else, something more predictable that doesn't conflict with the kernel's naming schema. For this example, I'm going to rename <code>eth0</code> to <code>internal0</code>. You can use any other name if you wish. The <code>/etc/network/interfaces</code> file will look something like the following after this change,  

```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback
#
# The primary network interface
allow-hotplug internal0
iface internal0 inet dhcp
#
# This is an autoconfigured IPv6 interface
iface internal0 inet6 auto

```

Save the changes made. Next, create an empty file called <code>/etc/systemd/network/10-persistent-net.link</code>,  

```bash
sudo touch /etc/systemd/network/10-persistent-net.link
```

Open it in your favorite text-editor and paste the following content to it,  

```bash
[Match]
MACAddress=b4:96:91:14:ae:5a

[Link]
Name=internal0

```

Of course, you'll need to change <code>b4:96:91:14:ae:5a</code> and <code>internal0</code> above with the MAC address of the interface you are configuring and the new persistent name you wish to give to it.  

Save the file and reboot the machine. Reboot is essential here for these changes to take effect.  

I hope this will be of help to a soul or two out there.  

![Debian](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/debian_wp.webp "Debian")  
<figcaption>Image courtesy Sohail & Hayderctee</figcaption>  
