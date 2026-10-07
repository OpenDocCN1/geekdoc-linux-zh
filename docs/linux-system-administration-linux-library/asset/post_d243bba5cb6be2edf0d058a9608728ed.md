
# Configuring an X Server

For very old cards, you may need to know what RAMDAC and clock chips the boards use. In all cases, you should know how much RAM the card boasts.

Monitor capabilities: You must know the maximum horizontal and vertical refresh rates of your monitor. You can obtain this information from the monitor's manual.

Desired resolutions: You'll be asked to specify what resolutions you want to use, as well as what color depths.

**TIP** Laptop computers can be particularly tricky for X, because laptop displays are unusually finicky about acceptable resolutions and display refresh rates. Check http://www.cs.utexas/users/kharker/linux-laptop/ for a collection of Linux users' experiences with various laptops. Most of these include ready-made XF86Config files you can use instead of building one yourself.

# XFree86 4.0

XFree86 4.0 is a major upgrade over version 3.3.6. This upgrade adds many features and entails substantial changes to XFree86 configuration. With luck, you won't have to concern yourself with these changes, because they'll be handled automatically at system installation. If you want to upgrade from 3.3.6 to 4.0, or if you need to modify your installation, you'll have to deal with these changes.

# Changes from XFree86 3.x

XFree86 4.0 offers several improvements over XFree86 3.x, including:

- **Multihead displays**: You can install multiple video cards in a single computer, attach them to monitors that you place next to each other, and have X create a virtual desktop that spans both displays.

- **New driver architecture**: In XFree86 3.x, each X server can contain one or more drivers for specific video cards. To use an S3 board, you'd use an X server called XF86_53; to use an ATI Mach64 board, you'd use XF86 Mach64. XFree86 4.0, by contrast, you use a single X server, XFree86, which loads a driver module (in /usr/X11R/lib/modules/drivers) for your specific video hardware. This design is likewise easier to extend, although you as a user and administrator are unlikely to notice much difference.

- **DDC support**: The Data Display Channel (DDC) is a protocol that's been standard in video hardware since the mid-1990s. It allows monitors to communicate their maximum refresh rates to video cards and video software. XFree86 3.x does not support DDC, so you must enter this information manually. XFree86 4.0 adds support for DDC.

![](img/4fb617eb648f87def380ef5d92052d01_576_0.png)

TrueType font support: XFree86 4.0 adds support for TrueType fonts (the standard font type in Microsoft Windows). In practice, TrueType fonts have been available in Linux for some time through separate font servers, as described shortly in "Configuring a Font Server." Built-in TrueType support is an added convenience.

DRI support: The Direct Rendering Interface (DRI) is a hardware acceleration standard that allows Linux programs to take advantage of video boards with 3-D hardware acceleration features. As of XFree86 4.0.1, only the 3dfxs chips are supported, but this support is likely to expand in 2001 and beyond.

New configuration file format: The new XFree86 options mandate a new configuration format. The configuration file may be called XF8Config, or it may be called XF8Config-4 on some systems (including Red Hat 7.0).

You can check whether you're running XFree86 4.0 by looking for a link X in /etc or /etc/X11. If this link points to /usr/X11/bin/XFree86, your system is configured to use XFree86 4.0. If the link points to some other file, your system uses 3.x or possibly a third-party X server (see the sidebar "Alternatives to XFree86").

# Configuring XFree86 4.0

For an administrator, the XFree86 4.0 change that's important is to change the configuration file format. The general organization of the new XF8Config file is similar to that 3.x's XF8Config, so you should read "The XF8Config File" earlier, for details. In addition, the new file adds a few extra sections:

- **ServerLayout**: This section defines some overarching features of the server. Specifically, this section binds specific input and output devices. Chances you won't need to adjust this section from its default.
- **Module**: This section specifies server modules you want loaded. Modules can provide functionality such as TrueType support and DRI support. You probably won't have to adjust this section of the file.
- **DRI**: If you're lucky enough to have a video card with 3-D acceleration features supported by XFree86, you can define who may access these features in this section. A line allows all users to access DRI functions:

`Mode 666`

In Red Hat 7.0, there's only one standalone X configuration utility: xf86cfg. This is an X-based configuration tool (see Figure 16.3). To configure X with this utility, you can right-click the icon for a component in the main section of the window and select Configure from the resulting pop-up menu.

# Figure 16.3 xf86cfg lets you configure XFree86 4.0 in a point-and-click fashion.

![](img/4fb617eb648f87def380ef5d92052d01_578_0.png)

**WARNING** xf86cfg assumes it works on /etc/X11/X86Config, not the /etc/X11/X86Config-4 file used by Red Hat 7.0. You must therefore temporarily rename the file, or create a link, to use this utility in Red Hat 7.0.

In addition to using xf86cfg, you can configure XFree86 4.0 by issuing the command **XFree86-configure**. This command creates a file called /root/X86Config.new, which should be at least minimally functional.

# Starting X Automatically

When you installed Linux, you may have been asked you wanted to start the OS in text mode or graphics mode. If you selected the former option, you see a text-based login and can launch X after logging in. If you selected the latter option, and if the system's configuration is correct, you should be greeted by an X-based login program. On older versions of Linux, this login was handled by a program known as the XDM. More recent versions of Linux use similar utilities that are associated with the KDE or GNOME projects (described shortly). These updated packages are known as the KDE Display Manager (KDM) and the GNOME Display Manager (GDM). All three programs serve a similar function, however: They let you on the computer. For simplicity's sake, the rest of this chapter refers to all programs as XDM.

# Networking and Troubleshooting

PART 5
