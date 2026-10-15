
and windows. Most office and home environments run Linux and X on their local machines. The more-enlightened companies and users harness the power of the networking features of X, enabling thin-client environments and allowing the use of customized desktops designed specifically for that company. Having applications launch from a single location makes the lives of system administrators a lot easier because they have to work on only one machine, rather than several.

## Using X

X.Org 7.3 is the X server that is used with Ubuntu. The base Xorg distribution consists of 30 packages (almost 120MB), which contain the server, along with support and development libraries, fonts, various clients, and documentation. An additional 1,000 or more X clients, fonts, and documentation are also included with Ubuntu.

### NOTE

A full installation of X and related X.Org 7.4 files can consume more—usually much more—than 170MB of hard drive space. This is because additional clients, configuration files, and graphics (such as icons) are under the /usr/bin and /usr/share directory trees. You can pare excessive disk requirements by judiciously choosing which X-related packages (such as games) to install on workstations. However, with the increased capacity of most desktop PC hard drives today, the size requirements are rarely a problem, except in configuring thin-client desktops or embedded systems.

The /usr directory and its subdirectories contain the majority of Xorg’s software. Some important subdirectories are

- /usr/bin—This is the location of the X server and various X clients. (Note that not all X clients require active X sessions.)
- /usr/include—This is the path to the files necessary for developing X clients and graphics such as icons.
- /usr/lib—This directory contains required software libraries to support the X server and clients.
- /usr/lib/X11—This directory contains fonts, default client resources, system resources, documentation, and other files that are used during X sessions and for various X clients. You will also find a symbolic link to this directory, named X11, under the /usr/lib directory.
- /usr/lib/modules—This path to drivers and the X server modules used by the X server enables use of various graphics cards.

The main components required for an active local X session are installed on your system if you choose to use a graphical desktop. These components are the X server, miscellaneous fonts, a terminal client (that is, a program that provides access to a shell prompt), and a

client known as a window manager. Window managers, which are discussed later in this chapter (see the section “Selecting and Using Window Managers”), administer screen displays, including overlapping and tiling windows, command buttons, title bars, and other onscreen decorations and features.

## Elements of the `xorg.conf` File

The most important file for Xorg is the xorg.conf configuration file, which can be located in the /etc/X11 directory. This file contains configuration information that is vital for X to function correctly, and is usually created during the installation of Ubuntu. Should you need to change anything post-install, you should use the system-config-display application, which we cover later in this chapter. Information relating to hardware, monitors, graphics cards, and input devices is stored in the xorg.conf file, so be careful if you decide to tinker with it in a text editor!

## Bullet Proof X

Ubuntu 8.04 LTS comes with a rather useful feature called Bullet Proof X. In short, it is designed to work no matter what may happen, so in the event of some cataclysmic event which destroys your main X system you will still have some graphical way of getting yourself back to a fully functional X-based system. Thanks to Bullet Proof X you shouldn’t need to edit your xorg.conf file, but it can be a good idea to understand what it is made up of, in case you ever need to troubleshoot an X problem.

Let’s take a look at the contents of the file so that you can get an idea of what X is looking for. The components, or sections, of the xorg.conf file specify the X session or server layout, along with pathnames for files that are used by the server, any options relating directly to the server, any optional support modules needed, information relating to the mouse and keyboard attached to the system, the graphics card installed, the monitor in use, and of course the resolution and color depth that Ubuntu uses. Of the 12 sections of the file, these are the essential components:

- **ServerLayout**—Defines the display, defines one or more screen layouts, and names input devices.
- **Files**—Defines the location of colors, fonts, or port number of the font server.
- **Module**—Tells the X server what graphics display support code modules to load.
- **InputDevice**—Defines the input devices, such as the keyboard and mouse; multiple devices can be used.
- **Monitor**—Defines the capabilities of any attached display; multiple monitors can be used.
- **Device**—Defines one or more graphics cards and specifies what optional features (if any) to enable or disable.
- **Screen**—Defines one or more resolutions, color depths, perhaps a default color depth, and other settings.
