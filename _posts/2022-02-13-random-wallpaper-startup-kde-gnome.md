---
layout: post
title: Set a random wallpaper at startup in KDE Plasma
categories: [wallpaper, KDE]
slug: random-wallpaper-startup-kde-gnome
---

I've been a Openbox & Xfce user most of my GNU/Linux life. Only recently, I've started using KDE Plasma. In Openbox one can easily run a command via its <code>autostart</code> file to set a random wallpaper,  

```bash
feh --no-fehbg --bg-scale --randomize path/to/the/wallpaper/directory/* &
```

Xfce makes it even easier as there already is an option to set a random wallpaper at startup in its settings.  
In KDE Plasma, I was unable to find any option to set a random wallpaper at the session startup so I came up with a little hack to achieve this.  
<!--more-->
I keep all my wallpapers in <code>$HOME/Pictures/Backgrounds</code> directory and this hack is hard-coded to this particular path so if you keep your wallpapers in some other location, you'll have to change this path accordingly. Any location is valid as long as you have write permissions for that location.  
First thing that we need to do is create a hidden directory <code>.default-background</code> in <code>$HOME/Pictures/Backgrounds</code> directory. To do so, open your favorite terminal emulator and run,  

```bash
mkdir $HOME/Pictures/Backgrounds/.default-background
```

Next, we need to create a <code>link</code> with the name of <code>default_background.jpeg</code> in this hidden directory to any wallpaper image file in the wallpaper directory. For this example I'm gonna pick a wallpaper image called <code>there-is-no-cloud.jpeg</code>,  

```bash
ln -Pfn $HOME/Pictures/Backgrounds/there-is-no-cloud.jpeg $HOME/Pictures/Backgrounds/.default-background/default_background.jpeg
```

Now, right click on KDE Plasma desktop and select <code>Configure Desktop and Wallpaper...</code>. Next, under the <code>Wallpaper</code> tab, click on <code>Add Image</code> option and select the link, <code>default_background.jpeg</code>, that we have just created by navigating to the <code>$HOME/Pictures/Backgrounds/.default-background</code> directory. After adding this, select it and hit the <code>Apply</code> button to set it as the desktop wallpaper.  
For our final step we need to create an empty file called <code>random_background.sh</code> in <code>/etc/X11/xinit/xinitrc.d</code> directory and make it executable,  

```bash
sudo touch /etc/X11/xinit/xinitrc.d/random_background.sh
sudo chmod 755 /etc/X11/xinit/xinitrc.d/random_background.sh
```

Open this empty file as root or with sudo permissions in your favorite text-editor and paste the following code snippet into it,  

```bash
#!/bin/sh

Backgrounds_Source="$HOME/Pictures/Backgrounds/"
Random_Background=$(find "$Backgrounds_Source" -type f -print0 | xargs -0 file --mime-type | grep -F 'image/' | cut -d ':' -f 1 | sort -R | head -n 1)
Background_Image="$HOME/Pictures/Backgrounds/.default-background/default_background.jpeg"

if [ -d "$Backgrounds_Source" ]; then

    if [ -n "$Random_Background" ]; then

	ln -Pfn "$Random_Background" "$Background_Image"

    fi
fi
```

Save the changes to the file.  

That's it! From now on, every time you log-in to a new session you'll be greeted by a new wallpaper.  

Just in case, someone was curious about that <code>there-is-no-cloud.jpeg</code> wallpaper,  

![There Is No Cloud](https://static.fsf.org/nosvn/stickers/thereisnocloud.svg "There Is No Cloud")

Don't hesitate to contact me if you have any question or confusion regarding this article or anything else on the blog.
