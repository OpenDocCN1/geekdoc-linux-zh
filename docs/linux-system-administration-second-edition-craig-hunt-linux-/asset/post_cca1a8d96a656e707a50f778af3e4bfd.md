
## Using an X Configuration Tool

As a general rule, it's easiest to create an XF86Config file using an X configuration tool. Hand-editing XF86Config may be useful when you change hardware, but creating a configuration file from scratch is a daunting task, even for X gurus. All major Linux distributions include X configuration tools that run during system installation. These tools are usually available after installation, as well. Examples include:

- **XFree86** The XFree86 4.x executable program, XFree86, can generate a starter configuration file. Type `XFree86 –configure` to create a file called /root/XF86Config.new, which should be at least minimally functional. You can then modify it via xf86cfg (described next) or manual editing, should you need to tweak it.
- **xf86cfg** This program is the standard GUI X configuration tool for XFree86 4.x. It's shown in Figure 13.2. To configure X with this utility, you can right-click the icon for a component in the main section of the window and select Configure from the resulting pop-up menu.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_341_0.png)

Figure 13.2: xf86cfg lets you configure XFree86 4.x in a point-and-click fashion.

> **Warning** Some versions of xf86cfg assume they should work on /etc/X11/XF86Config, not /etc/X11/XF86Config-4. You might therefore need to temporarily rename the file, or create a link, to use this utility. This was true in Red Hat 7.0, for instance, but not in Red Hat 7.3.

- **xf86config** This is the crustiest of the common XFree86 3.3.x configuration tools. It runs entirely in text mode, and asks you a series of questions about your hardware and desired configuration. There is no possibility to go back and correct an error, so you must kill the program and start again if you make a mistake. Because of its crude user interface, xf86config can be used before X is running or if X is seriously misconfigured. This program also provides more control over the contents of XF86Config than do most configuration tools, which is helpful with some unusual hardware.
- **Xconfigurator** This program is another text-mode XFree86 3.3.x configuration tool. Unlike xf86config, though, Xconfigurator uses color text and text-mode dialogs rather than simple streams of text. This makes Xconfigurator easier to use.
- **XF86Setup** This is an X-based configuration tool for XFree86 3.3.x. You can therefore use this utility to reconfigure an X server that’s working nonoptimally, but you can’t use it to get X working at the outset.

> **Note** Most distributions include GUI X configuration tools that run during system installation. These tools typically start the system in a lowest-common-denominator VGA resolution in order to collect information. Chapter 2 includes information on X configuration during system installation, but details vary substantially from one distribution to another.

You should have several pieces of information handy before you begin configuring your X server. Although some configuration utilities can probe for some of this information, you’ll need to know some of it yourself. These critical features are as follows:

- **Mouse type** Most modern computers use a PS/2 mouse, but there are several other options, such as Logitech and Microsoft mouse protocols.
- **Mouse device** Most distributions create a link so that you can access a mouse as /dev/mouse. You may need to do the same, or specify the mouse device directly. /dev/psaux is the usual device file for PS/2 mice. Serial mice can usually be addressed as /dev/ttyS0 or /dev/ttyS1.
- **Video card information** Some X configuration utilities let you select a card from a long list of model names. Others require you to know the chipset used on the card. For very old cards, you may need to know what RAMDAC and clock chips the boards use. Knowing how much RAM the card boasts may be necessary for some cards.
- **Monitor capabilities** You should know the maximum horizontal and vertical refresh rates of your monitor. You can obtain this information from the monitor’s manual. If your system uses XFree86 4.x and the monitor was built in the late 1990s or later, XFree86 can obtain this information via DDC.
- **Desired resolutions** You’ll be asked to specify what resolutions you want to use, as well as what color depths.

> **Tip** Laptop computers and desktop LCD monitors can be particularly tricky to configure for X, because these displays are unusually finicky about acceptable resolutions and display refresh rates. Check http://www.linux–laptop.net/ for a collection of links to Linux users' experiences with various laptops. Most of these include ready–made XF86Config files you can use instead of building one yourself.

## Alternatives to XFree86

XFree86 is the most common X server in Linux, but it’s not the only one available for Linux, nor is it the most common outside of the Linux world. Two commercial X servers are available for Linux: Xi Graphics’ Accelerated X (http://www.xig.com/) and MetroLink’s Metro–X (http://www.metrolink.com/). Both servers offer an assortment of features that are useful in certain specific situations, such as multiscreen and touch–screen support. These servers also sport somewhat different lists of supported hardware than does XFree86, so you may want to use a commercial server with some video hardware. Commercial X servers for Linux use a configuration file similar to XF86Config, but their details differ. Consult the software’s documentation to learn how to configure it.

Non–Linux systems frequently use X servers other than XFree86. Commercial Unixes often ship with their own X servers. X servers are also available for non–Unix systems, such as Windows and MacOS. Examples include Hummingbird’s eXceed (http://www.hcl.com/products/nc/exceed/), StarNet’s X–Win32 (http://www.starnet.com/), NetSarang’s Xmanager (http://www.netsarang.com/), Tenon’s Xtools (http://www.tenon.com/products/xtools/), and PowerLAN’s eXodus (http://www.powerlan–usa.com/exodus.html). These programs typically use GUI configuration utilities. Those that run inside the host OS’s GUI (such as all the Windows and Macintosh products) typically don’t require special mouse or video configuration. They usually do require font configuration, however, and often offer features that are meaningless in Linux, such as the ability to run an X session within a single host OS window.

If you run a network and want to provide X–based access to multiple users, an X *terminal* is another X option you may want to investigate. An X terminal is a computer that’s specialized to run X. Such a computer has little memory, no hard disk, and an anemic CPU. X servers typically include large color displays. The "NCD X–Terminal Mini–HOWTO" document covers many details of X terminal configuration.

## Starting X Automatically

When you installed Linux, you may have been asked whether you wanted to start the OS in text mode or graphics mode. If you selected the former option, you see a text–based login prompt and can launch X only after logging in. If you selected the latter option, and if the system’s X configuration is correct, you should be greeted by an X–based login program wherever you start the system. On older versions of Linux, this X–based login was handled by a program known as the *X Display Manager* (XDM). More recent versions of Linux typically use similar utilities that are associated with the KDE or GNOME projects (described shortly). These updated packages are known as the *KDE Display Manager* (KDM) or the *GNOME Display Manager* (GDM). All three programs serve a similar function, however: They let you log on to the computer. For simplicity’s sake, the rest of this chapter refers to all these programs as *XDM*.

Whether the computer boots into text or graphics mode is handled by the /etc/inittab startup script. Near the start of this script, you should find a line that resembles the following:
