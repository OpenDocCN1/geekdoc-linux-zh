
## Configuring Software Repositories

Ubuntu uses software repositories to get information about available software that can be installed onto your system. By default, it only allows access to a small portion of software (even though this software is officially supported by Ubuntu). However, Ubuntu is based on a much older Linux distribution called Debian. Debian has access to more than 17,000 different packages, which means that Ubuntu can have access to these packages, too.

To enable this, you need to use the other GUI wrapper for Ubuntu, called synaptic. You can find it under the System, Administration, Synaptic Package Manager option. After you have entered your password when prompted and synaptic has appeared, you can access repository information through the Settings menu, Repositories option. Several options display here, and normally the defaults suffice. However, a lot of the software described in this book requires extra repositories to be enabled for you to access the software.

Simply click on the first option, Ubuntu 6.06 LTS (Binary), and click the Edit button on the right side to see the screen shown in Figure 4.2. Here you can tick the Universe and Multiverse repositories to enable you to download software from the wider Debian software universe and some nonfree software such as proprietary drivers and codecs.

![](img/e464b828c497c99e41f61d4c55f1c0db_97_0.png)

FIGURE 4.2 Enable both Universe and Multiverse repositories to allow access to a huge variety of software for Ubuntu.

For each binary entry, there is an associated source entry that Ubuntu sometimes uses to retrieve source code information. Make sure to update the matching source entry, but be aware that it is done slightly differently than with the binary repositories. Instead of ticking boxes, you must actually type some information. Don't worry, all you need to enter are the words universe and multiverse separated by a space, as shown in Figure 4.3.

![](img/e464b828c497c99e41f61d4c55f1c0db_98_0.png)

FIGURE 4.3 Always remember when updating binary repositories to ensure that the paired source repository contains the same information.

## Installing Graphics Drivers

Ubuntu is extremely good at detecting and configuring graphics cards. However, it does struggle a bit with 3D support, mainly because you have to install proprietary drivers to enable full 3D support. Fortunately, this is an easy task to do, and we will do it at the command line.

Open up a terminal window as described earlier and use the following command:

```
$ sudo apt-get install drivername configtool
```

Change drivername and configtool depending on your graphics card. For Nvidia-based cards you need to change them to nvidia-glx and nvidia-settings, respectively; for ATI-based cards, use xorg-driver-fglrx and fglrx-control. APT intelligently detects any other required packages and installs them as necessary.

After APT has finished, you must do some minor work on the xorg.conf file, which is the file that X uses to configure itself. Use the following command to open up that file in the Text Editor, an easy-to-use GUI editor, and look for the Devices section:

```
$ sudo gedit /etc/X11/xorg.conf
```

Specifically, you are looking for the driver line because you need to make a slight modification to it, which is different for ATI and Nvidia cards. For ATI cards, you need to make sure that it looks like this:

```
Driver "fglrx"
```

For Nvidia, it needs to look something like this:

```
Driver "nvidia"
```

These entries tell X to use either the ATI or Nvidia driver that you have installed. All that remains is for you to restart your computer to allow Ubuntu to load the new drivers. Log back in to Ubuntu and open a terminal window. For Nvidia cards, type glxgears or for ATI fgl_glxgears (Figure 4.4) to bring up a small window that contains colored spinning gears. Seeing this means that your drivers have been installed correctly and 3D acceleration has been enabled.

![](img/e464b828c497c99e41f61d4c55f1c0db_99_0.png)

FIGURE 4.4 Who’d have believed that something as simple as spinning gears could bring so much joy? Seeing this means that your graphics card is ready for 3D action.

Now that you have your 3D acceleration configured, head on over to Chapter 13, “Games,” to see how Linux can handle the likes of Doom 3 and Quake 4, both of which require 3D acceleration.

## Changing Ubuntu’s Look and Feel

GNOME, the default window manager for Ubuntu, has a number of options to change how it looks and feels. The default theme is UbuntuLooks; this takes a blend of the GNOME Clearlooks theme, mixes it with icons from the Tango Project, and adds a little spice direct from Ubuntu. However, it is not to everyone’s taste, so in this section we look at changing the visual style of Ubuntu.
