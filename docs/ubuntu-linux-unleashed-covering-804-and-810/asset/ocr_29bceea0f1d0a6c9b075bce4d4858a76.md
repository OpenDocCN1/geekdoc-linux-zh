and windows. Most office and home environments run Linux and X on their local machines. The more-enlightened companies and users harness the power of the networking features of X, enabling thin-client environments and allowing the use of customized desktops designed specifically for that company. Having applications launch from a single location makes the lives of system administrators a lot easier because they have to work on only one machine, rather than several.

# Using X

X.Org 7.3 is the X server that is used with Ubuntu. The base Xorg distribution consists of 30 packages (almost 120MB), which contain the server, along with support and development libraries, fonts, various clients, and documentation. An additional 1,000 or more X clients, fonts, and documentation are also included with Ubuntu.

# NOTE

A full installation of X and related X.Org 7.4 files can consume more—usually much more—than 170MB of hard drive space. This is because additional clients, configuration files, and graphics (such as icons) are under the /usr/bin and /usr/share directory trees. You can pare excessive disk requirements by judiciously choosing which X-related packages (such as games) to install on workstations. However, with the increased capacity of most desktop PC hard drives today, the size requirements are rarely a problem, except in configuring thin-client desktops or embedded systems.

The /usr directory and its subdirectories contain the majority of Xorg’s software. Some important subdirectories are

+   - /usr/bin—This is the location of the X server and various X clients. (Note that not all X clients require active X sessions.)
+   - /usr/include—This is the path to the files necessary for developing X clients and graphics such as icons.
+   - /usr/lib—This directory contains required software libraries to support the X server and clients.
+   - /usr/lib/X11—This directory contains fonts, default client resources, system resources, documentation, and other files that are used during X sessions and for various X clients. You will also find a symbolic link to this directory, named X11, under the /usr/lib directory.
+   - /usr/lib/modules—This path to drivers and the X server modules used by the X server enables use of various graphics cards.

The main components required for an active local X session are installed on your system if you choose to use a graphical desktop. These components are the X server, miscellaneous fonts, a terminal client (that is, a program that provides access to a shell prompt), and a