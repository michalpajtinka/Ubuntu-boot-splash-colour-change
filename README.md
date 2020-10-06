I am using Ubuntu 19.10 and I really like Ubuntu very much, but I really don't like that purple colour everywhere. It was easy to chage desktop theme, but a bit more difficult to change colour of Plymouth boot splash. You can install other available boot splash by installing another packages, or you can create new theme by updating the current one. Here is some help:

This is based on the _khAttAm_ blog which has a bit outdated paths, but otherwise is still working.
https://www.khattam.info/howto-change-ubuntu-pinkpurple-plymouth-boot-screen-to-any-color-you-like-2010-11-09.html

# 1. Make a copy of the plymouth theme:
---
```
sudo cp -R /usr/share/plymouth/themes/ubuntu-logo /usr/share/plymouth/themes/ubuntu-logo-nonpink
```
# 2. Edit the name and location information:
---
```
sudo nano /usr/share/plymouth/themes/ubuntu-logo-nonpink/ubuntu-logo.plymouth
```

I have changed these lines:
```
Name=Ubuntu Logo NonPink

ImageDir=/usr/share/plymouth/themes/ubuntu-logo-nonpink

ScriptFile=/usr/share/plymouth/themes/ubuntu-logo-nonpink/ubuntu-logo.script
```
# 3. Edit the color in script:
---
```
sudo nano /usr/share/plymouth/themes/ubuntu-logo-nonpink/ubuntu-logo.script
```

I have changed these lines:
```
Window.SetBackgroundTopColor (0.85, 0.85, 0.85);

Window.SetBackgroundBottomColor (0.75, 0.75, 0.75);
```
Set those numbers as you like - take R, G and B decimal values from RGB code of colour you like and divide them with 256.

# 4. Edit the Ubuntu Logo:
---
```
sudo gimp /usr/share/plymouth/themes/ubuntu-logo-nonpink/ubuntu-logo.png
```

Original white logo on light grey backgroud wouldn't look well, so you can invert colours in this picture to get black variant. Or download new picture, for example Tux pinguin, replace that file with the new one (of course you have to rename the new file to ubuntu_logo.png).

# 5. Change the progress dots:
---
```
sudo gimp /usr/share/plymouth/themes/ubuntu-logo-nonpink/progress-dot-on.png
```
```
sudo gimp /usr/share/plymouth/themes/ubuntu-logo-nonpink/progress-dot-off.png
```

Again, change those as you like. I do not reccomend just to convert those to greyscale, because while the colour is nice, it looks like the dot is shining out grey.

# 6. Install the theme:
---
```
sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/ubuntu-logo-nonpink/ubuntu-logo.plymouth 100
```

# 7. Set the theme as default:
---
```
sudo update-alternatives --config default.plymouth
```

# 8. Update Initial Boot Image:
---
```
sudo update-initramfs -u
```

# Change grub background-color:
```bash
sudo nano /usr/share/plymouth/themes/ubuntu-logo-nonpink/ubuntu-logo.grub
sudo update-grub
```

# Change lock-screen background-color:
search for #lockDialogGroup
```bash
sudo nano /usr/share/gnome-shell/theme/gnome-shell.css
```

# Change login screen after boot:
search for #lockDialogGroup
```bash
sudo nano /etc/alternatives/gdm3.css
```

### Notation to set image as background:
```css
background: url(file:///usr/share/backgrounds/mybackground.png);
background-repeat: no-repeat;
background-size: cover;
background-position: center;
```
