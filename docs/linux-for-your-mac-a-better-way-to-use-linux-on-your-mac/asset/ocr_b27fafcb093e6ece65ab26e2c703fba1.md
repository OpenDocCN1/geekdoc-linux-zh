clients and utilities, 100 graphics, and 1,200 pages of documentation. A typical installation requires more than 70MB of hard drive space, and even more if additional X11 clients are installed.

# ## Features of X11

X is a portable graphical network interface for Linux, and works well on a stand-alone workstation, or as a graphics system for a large network. X works over slow serial dial-up lines or high-speed fiber-optic networks, and can easily serve one to 10,000 users. X provides for font management, the use of color and system- or client-specific *resources* or configuration files, includes source code, supports standardized command-line interfaces for clients known as *X Toolkit Options*, and has graphics device independence over a network.

Best of all, X is royalty free! Developers can build and distribute clients without licensing restrictions. And because of X’s portability, the version of XFree86 that runs on your Apple Macintosh has many of the same features as the version of X11 for an Intel-based PC, SPARC, or Alpha CPU.

This also means that any clients you develop on your PowerPC using X will nearly always build, install, and run exactly the same way on any other hardware platform supporting X.

# ## Configuring X11

Configuring X is one of the essential tasks of completing a successful Linux installation. Now an integral part of the install process for a majority of PowerPC Linux distributions, X configuration can generally be accomplished automatically as part of the install or booting process. This is great when everything goes OK, but if you run into problems, you may need to resort to one or more software tools to get things right.

# ## X under PPC Linux

Properly configuring X to work with your Mac’s hardware involves the creation of a file named *XF86Config*. This file may be located under the */root/,/etc,/etc/X11*, or */usr/X11R6/lib/X11* directories, and contains settings that match your computer’s graphics hardware (such as monitor frequencies and graphics card chipset information).

For X and the PowerPC, many installations default to using a *frame-buffer* server, in which the graphics hardware is modeled using the buffer memory of the computer’s video hardware. All drawing is handled at a high level, so that X and its clients do not need to know the specifics of the graphics hardware. While this