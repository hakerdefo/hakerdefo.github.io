---
layout: post
title: How to spice up Grub2 boot menu screen with colors & image
categories: [how-to, linux]
slug: grub2-customize-menu-screen-colors-image
---

The default look of Grub2 boot menu screen is a bit bland & boring to say the least, but it is very easy to spice it up with vivid font colors and a background image. Are you guys & gals ready to color your Grub2 boot menu screen? Let's dive right into it, then.  
<!--more-->

First, we need to create an empty file in the <code>/etc/grub.d/</code> directory with the name of <code>99_custom-colors</code>,  

```bash
sudo touch /etc/grub.d/99_custom-colors
```

Next, we need to make it executable,  

```bash
sudo chmod 755 /etc/grub.d/99_custom-colors
```

Now it's time to add some colors. Currently, Grub2 supports,  

 - Normal foreground and background terminal colors for fonts on the Grub2 screen aka <code>color_normal</code>  
 - Normal foreground and background terminal colors for Grub2 menu fonts aka <code>menu_color_normal</code>  
 - Highlight foreground and background terminal colors for fonts on the Grub2 screen aka <code>color_highlight</code>  
 - Highlight foreground and background terminal colors Grub2 menu fonts aka <code>menu_color_highlight</code>  

The following colors are supported,  

 - black  
 - blue  
 - green  
 - cyan  
 - red  
 - magenta  
 - brown  
 - light-gray  
 - dark-gray  
 - light-blue  
 - light-green  
 - light-cyan  
 - light-red  
 - light-magenta  
 - yellow  
 - white  

Foreground and background terminal colors are separated by a slash <code>/</code>. You can use any of the supported colors as you wish, for this tutorial I'm going to keep it relatively simple and use three colors, white, black and green. Remember the file <code>/etc/grub.d/99_custom-colors</code> we created earlier? It's time to open it and set the colors. Use your favorite text-editor to open it and paste the following snippet into it,  

```bash
echo "set color_normal=white/black"
echo "set color_highlight=green/black"
echo "set menu_color_normal=white/black"
echo "set menu_color_highlight=green/black"
```

GRUB2 treats the color <code>black</code> differently when it is set as a background color, like in the above example <code>color_normal=white/black</code>. In such a case, <code>black</code> is considered a value for <code>transparency</code> and the underlying image will be visible rather than the color <code>black</code>.  

Save the file.  

Now let's add an image to the background of Grub2 menu screen. Grub2 supports <code>PNG</code>, <code>JPEG</code> and <code>TGA</code> image files. For this example, I'm using the following image by Máirín Duffy,  

![Grub2 Background Image](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/grub_demo_background.jpg "Grub2 Background Image")
<figcaption>Image courtesy Máirín Duffy</figcaption>  

You can download and use the above image, or you can use any other image if you wish. Copy the image to either <code>/usr/share/backgrounds</code> or <code>/usr/share/wallpapers</code> directory. For this example, I'm gonna call this image <code>grub_demo_background.jpg</code> and save it in the <code>/usr/share/backgrounds</code> directory. Next, open the file <code>/etc/default/grub</code> in your favorite text-editor and append this line to it,  

```bash
GRUB_BACKGROUND=/usr/share/backgrounds/grub_demo_background.jpg
```

Also, make sure that the <code>GRUB_TERMINAL</code> and <code>GRUB_GFXMODE</code> variables are uncommented and set to the following values in this file,  

```bash
GRUB_TERMINAL="gfxterm"
GRUB_GFXMODE="auto"
```

Save the changes made to <code>/etc/default/grub</code> file.  

And, finally, run the following command to apply these changes to the Grub2 configuration,  

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

Reboot the machine to test your newly spiced up Grub2 screen.  

Rather than rebooting to test various color combinations, you can play with various colors by using GRUB2's command line during the boot process. When the GRUB2 screen appears, press any key to stop the countdown timer and press <code>C</code> to enter the GRUB2 command line. You can play around with different color combinations by running <code>set</code> command with different Grub2 color options like this,  

```bash
set color_normal=yellow/black  
set color_highlight=black/yellow  
set menu_color_normal=black/light-gray  
set menu_color_highlight=yellow/dark-gray  
```

Changes made to the font colors are applied immediately after the command. Pressing the <code>Esc</code> key will return you to the main Grub2 screen, and here you can view the full effect of changes made to the look of the Grub2 menu screen. You can press <code>C</code> again to go back to the command line and test some more color combinations if you wish. Please remember that the changes made via the Grub2 command line are not saved, and the settings will get restored to their defaults once you leave the Grub2 menu screen. You'll need to make these changes permanent using the method discussed above in the article.  

If you want to create a complete Grub2 theme from the scratch, I highly encourage you to read this article by Vladimir Testov,  

[Grub2 theme tutorial by Vladimir Testov](http://wiki.rosalab.ru/en/index.php/Grub2_theme_tutorial){:target="_blank"}  
