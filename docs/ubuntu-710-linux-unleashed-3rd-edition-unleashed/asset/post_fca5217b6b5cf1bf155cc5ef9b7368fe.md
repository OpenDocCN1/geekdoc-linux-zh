
## NOTE

What better way to demonstrate the capability of X to handle remote clients than by using its capabilities to produce this chapter. Although the OpenOffice.org file for this chapter resided on a Mac mini (running Ubuntu), the display and keyboard used were actually part of an Acer Ferrari notebook running Ubuntu 7.04 LTS, via an ethernet connection. Revisions were done using a Logitech keyboard and mouse of a desktop machine running Ubuntu 6.06.1, again connected to the Mac mini via X, but this time using a wireless connection.

Because X offers users a form of distributed processing, this means that Ubuntu can be used as a very cheap desktop platform for clients that connect to a powerful X server. The more powerful the X server, the larger the number of X-based clients that can be accommodated. This functionality can breathe new life into older hardware, pushing most of the graphical processing on to the server. A fast network is a must if you intend to run many X clients because X can become bandwidth-hungry.

X is hugely popular in the UNIX and Linux world for a variety of reasons. The fact that it supports nearly every hardware graphics system is a strong point, as well as strong multi-platform programming standards give it a solid foundation of developers committed to X. Another key benefit of X is its networking capability, which plays a central point in administration of many desktops and can also assist in the deployment of a thin-client computing environment. Being able to launch applications on remote desktops and also standardize installations serve to highlight the versatility of this powerful application.

More recent versions of X have also included support for shaped windows (that is, non-rectangular), graphical login managers (also known as display managers), and compressed fonts. Each release of X brings more features designed to enhance the user experience, including being able to customize how X client applications appear, right down to buttons and windows. Most office and home environments run Linux and X on their local machines. The more-enlightened companies and users harness the power of the networking features of X, enabling thin-client environments and allowing the use of customized desktops designed specifically for that company. Having applications launch from a single location makes the lives of system administrators a lot easier because they have to work on only one machine, rather than several.

## Using X

X.Org 7.3 is the X server that is used with Ubuntu. The base Xorg distribution consists of 30 RPM packages (almost 120MB), which contain the server, along with support and development libraries, fonts, various clients, and documentation. An additional 1,000 or more X clients, fonts, and documentation are also included with Ubuntu.

## NOTE

A full installation of X and related X.Org 7.3 files can consume more—usually much more—than 170MB of hard drive space. This is because additional clients, configuration files, and graphics (such as icons) are under the /usr/bin and /usr/share directory trees. You can pare excessive disk requirements by judiciously choosing which X-related packages (such as games) to install on workstations. However, with the increased capacity of most desktop PC hard drives today, the size requirements are rarely a problem, except in configuring thin-client desktops or embedded systems.

The /usr directory and its subdirectories contain the majority of Xorg’s software. Some important subdirectories are

- /usr/bin—This is the location of the X server and various X clients. (Note that not all X clients require active X sessions.)
- /usr/include—This is the path to the files necessary for developing X clients and graphics such as icons.
- /usr/lib—This directory contains required software libraries to support the X server and clients.
- /usr/lib/X11—This directory contains fonts, default client resources, system resources, documentation, and other files that are used during X sessions and for various X clients. You will also find a symbolic link to this directory, named X11, under the /usr/lib directory.
- /usr/lib/modules—This path to drivers and the X server modules used by the X server enables use of various graphics cards.

The main components required for an active local X session are installed on your system if you choose to use a graphical desktop. These components are the X server, miscellaneous fonts, a terminal client (that is, a program that provides access to a shell prompt), and a client known as a window manager. Window managers, which are discussed later in this chapter, administer onscreen displays, including overlapping and tiling windows, command buttons, title bars, and other onscreen decorations and features.

## Elements of the xorg.conf File

The most important file for Xorg is the xorg.conf configuration file, which can be located in the /etc/X11 directory. This file contains configuration information that is vital for X to function correctly, and is usually created during the installation of Ubuntu. Should you need to change anything post-install, you should use the system-config-display application, which we will cover later in this chapter. Information relating to hardware, monitors, graphics cards, and input devices is stored in the xorg.conf file, so be careful if you decide to tinker with it in a text editor!
