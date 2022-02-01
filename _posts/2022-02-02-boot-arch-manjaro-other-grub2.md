---
layout: post
title: How to boot Arch Linux or Manjaro from Grub2 of other distribution
categories: [how-to, grub2]
slug: boot-arch-manjaro-other-grub2
---

## Problem:

You installed Arch Linux or Manjaro or any other Arch derivative but you didn't install Grub2 on the MBR of your HDD as you already have Grub2 installed there and you want to control the boot process from already installed Grub2 instance but booting Arch or Manjaro via that Grub2 menu is ending in kernel panic.  

## Solution:

I recently installed Manjaro and during the install process, chose to install Grub2 on the root partition instead of MBR as I already have Grub2 installed there and I wanted to keep it that way. After installation, I booted into my Debian install which controls the Grub2 on the MBR and ran,  
```bash
sudo update-grub2
```
And Grub2 did pick up my fresh Manjaro install and added it to its menu. I rebooted the computer and from Grub2 menu, selected Manjaro but much to my surprise and disappointment the boot process was halted by kernel panic error. Upon a bit of research, I discovered that Manjaro and its parent distro Arch Linux, provides Intel and AMD microcode as a separate image and this results in multiple initramfs images. These multiple images confuse the Debian's Grub2 and depending on your processor it only lists either Intel microcode image or AMD microcode image in its menu. For example Grub2 on my system lists following in its menu entry for Manjaro,  
```bash
initrd /boot/intel-ucode.img
```
As you can see the real initramfs image is missing and this is the reason the boot process ends in kernel panic as it fails to find the initial ramdisk. The correct Grub2 entry should list both the microcode image and the actual initramfs as Grub2, since v2.03, is capable of supporting multiple initramfs images. The ideal entry in case of my Manjaro install should look like this,  
```bash
initrd /boot/intel-ucode.img /boot/initramfs-5.10-x86_64.img
```
Solution for this problem involves two steps. First step is to prevent Grub2 from creating menu entry for Manjaro or Arch and then in second step we need to manually chain-load that Manjaro or Arch install.  
First we need to get UUID of the partition where Arch or Manjaro is installed. One way of finding this is running this command in terminal,  
```bash
lsblk -f
```
I've installed Manjaro on <code>sda1</code> and the UUID of that partition is <code>1234567a-ab12-123a-1234-ab12345a1234</code>. Next we need to edit <code>/etc/default/grub</code> file and add the following line to it,  
```bash
GRUB_OS_PROBER_SKIP_LIST="1234567a-ab12-123a-1234-ab12345a1234@/dev/sda1"
```
You will need to change the UUID and the partition name as per your system. It's <code>UUID@/dev/partition</code> in short.  
In our final step we need to manually chain-load the Arch or Manjaro entry in our Grub2 menu. This can be done via editing <code>/etc/grub.d/40_custom</code> file. You'll need to convert the partition name to the Grub2 schema but it's not that hard. For example <code>sda1</code> will become <code>hd0,msdos1</code> for MBR partition table and <code>hd0,gpt1</code> for GUID partition table. Similarly <code>sda2</code> will become <code>hd0,msdos2</code> for MBR partition table and <code>hd0,gpt2</code> for GUID partition table and <code>sdb2</code> will become <code>hd1,msdos2</code> for MBR partition table and <code>hd1,gpt2</code> for GUID partition table. In my case Manjaro in installed on <code>sda1</code> and my partition table is MBR so the following code will go into the <code>/etc/grub.d/40_custom</code> file,  
```bash
menuentry "Manjaro" {
	set root=hd0,msdos1
	chainloader +1
}
```
After saving the changes, all we need to do is run,  
```bash
sudo update-grub2
```
The manually added Manjaro entry will be the last item on Grub2 menu and it'll chain-load the Manjaro's Grub2, which will boot into Manjaro without a hitch.  

Happy booting!  
