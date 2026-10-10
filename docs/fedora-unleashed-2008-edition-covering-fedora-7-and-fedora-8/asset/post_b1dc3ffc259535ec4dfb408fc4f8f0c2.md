
X.Org was forked when a disagreement broke out over certain restrictions that were going to be included in the XFree86 license. Taking a snapshot of code that was licensed under the previous version of the license, X.Org drove forward with its own implementation based on the code. Almost in unison, most Linux distributions turned their back on XFree86 and switched their development and efforts to X.Org.

In this chapter, you learn how to work with GNOME and also the version of X that is included with Fedora. We look at the fundamentals of X and how to get X to work with any upgrades that might affect it, such as a new graphics card or that new flat-panel display you just bought. We also take a look at some of the other Window Managers that are included with Fedora, including KDE and Xfce.

## The Red Hat and Fedora Desktop

> If you have used earlier versions of Fedora and indeed Red Hat Linux, you will be more than aware of Bluecurve and perhaps also Clearlooks. Fedora has now settled on a consistent style throughout the whole distribution and has finally done away with the slightly older-looking Bluecurve icon set in favor of the Nodoka theme. KDE, another window manager you’ll learn about later, has also received some polish, and the two window managers have a consistent look and feel.

## The GNOME Desktop Environment

A desktop environment for X provides one or more window managers and a suite of clients that conform to a standard graphical interface, based on a common set of software libraries. When they are used to develop associated clients, these libraries provide graphical consistency for the client windows, menus, buttons, and other onscreen components, along with some common keyboard controls and client dialogs. The following sections discuss the primary desktop environment that is included with Fedora: GNOME.

The GNOME project, which was started in 1997, is the brainchild of programmer whiz Miguel de Icaza. GNOME provides a complete set of software libraries and clients. GNOME depends on a window manager that is GNOME-aware. This means that to provide a graphical desktop with GNOME elements, the window manager must be written to recognize and use GNOME. Some compliant window managers that are GNOME-aware include Havoc Pennington’s *metacity* (the default GNOME window manager), Enlightenment, Compiz, Window Maker, and IceWM.

Fedora uses GNOME’s user-friendly suite of clients to provide a consistent and user-friendly desktop. GNOME is a stable feature of Red Hat Enterprise Linux distribution and Fedora because Red Hat actively supports its development. GNOME clients are found under the `/usr/bin` directory, and GNOME configuration files are stored under the `/etc/GNOME` and `/usr/share/GNOME` directories, with user settings stored in the home directory under `.GNOME` and `GNOME2`.

A representative GNOME desktop, running the removable media preferences tool used for setting actions to events, is shown in Figure 3.1.

![](img/34e72348d53ca54c2a1d9c871316691b_84_0.png)

**FIGURE 3.1** Fedora's GNOME desktop uses the *metacity* window manager and offers a selection of GNOME themes.

You can configure your desktop in various ways and by using different menu items under the Preferences menu, which can be found as part of the main Desktop menu. With the myriad configuration options, you can tailor every aspect of your system's look and feel. Figure 3.2 shows a selection of the Preferences options available to you.

![](img/34e72348d53ca54c2a1d9c871316691b_84_1.png)

**FIGURE 3.2** You can customize your Fedora desktop by using the Preferences settings that are available in the System, Preferences menu.

## AIGLX—Eye Candy for the Masses

Recent development work carried out on X has allowed the introduction of a number of hardware-accelerated effects within Fedora and its window managers. No longer do you have to drool at your Mac OS X-using colleagues when they work; now Fedora has a whole load of "wow" effects designed to add that professional touch to Linux. Up until recently, enabling these desktop effects has required a lot of work, including downloading specific packages and using the console to configure some of them. However, with Fedora 8, all of this has been done away with, and there is very little that you need to do to get access to the effects.

If you want the flashy effects, Fedora relies upon the alternate Compiz window manager, which to most end users does not appear any differently than metacity, the standard window manager in use by Fedora. You need to make sure you have the latest version of drivers for your graphics card/chipset; we cover this in Chapter 9, "Games."

### NOTE

You might wonder why installation of graphics drivers is placed alongside information on games. For the most part, 3D acceleration is not a necessity if you are using Fedora for productivity only. However, if you are intending to work off a bit of aggression by blowing away some opponents in Unreal Tournament, you are going to need 3D acceleration enabled, and you need the specific graphics drivers for that.

After you have verified your graphic driver situation, you will find a menu option under System, Preferences, Look and Feel, called Desktop Effects (see Figure 3.3). Open it and select the option to Enable Desktop Effects. After a couple of seconds, you may see your window decorations (title bar, minimize and maximize buttons) disappear and then reappear. It may seem that nothing has happened, but check the box to activate Wobbly Windows and then grab hold of the window title bar and move it around. If everything has gone according to plan, it should wobble! Click Keep Settings to save the settings, and welcome to a world of fancy effects.

![](img/34e72348d53ca54c2a1d9c871316691b_85_0.png)

**FIGURE 3.3** Use the Desktop Effects tool to set the scene for some snazzy 3D effects.

The "wobbly windows" are the most obvious effect, and it provides a fluid effect when you move your windows around the desktop area. Or if you hold down the Ctrl and Alt keys and press either the left or right cursor button, your desktop should move as if it is part of a cube, taking you from one virtual desktop to another.

This technology is still very much in its infancy, so expect great things in future versions!

## Basic X Concepts

The underlying engine of X11 is the X protocol, which provides a system of managing displays on local and remote desktops. The protocol uses a client/server model that allows an abstraction of the drawing of client windows and other decorations locally and over a network. An X server draws client windows, dialog boxes, and buttons that are specific to the local hardware and in response to client requests. The client, however, does not have to be specific to the local hardware. This means that system administrators can set up a network with a large server and clients and enable users to view and use those clients on workstations with totally different CPUs and graphics displays.

> **NOTE**
> We couldn't think of a better way to demonstrate the capability of X to handle remote clients than by using its capabilities to produce this chapter. Although the OpenOffice.org file for this chapter resided on a Mac mini (running Fedora), the display and keyboard used were actually part of an Acer Ferrari notebook running Ubuntu 6.06 LTS, via an ethernet connection. Revisions were done with the Logitech keyboard and mouse of a desktop machine running Fedora 8, again connected to the Mac mini via X, but this time using a wireless connection.

Because X offers users a form of distributed processing, this means that Fedora can be used as a very cheap desktop platform for clients that connect to a powerful X server. The more powerful the X server, the larger the number of X-based clients that can be accommodated. This functionality can breathe new life into older hardware, pushing most of the graphical processing on to the server. A fast network is a must if you intend to run many X clients because X can become bandwidth-hungry.

X is hugely popular in the UNIX and Linux world for a variety of reasons. It supports nearly every hardware graphics system, and strong multiplatform programming standards give it a solid foundation of developers committed to X. Another key benefit of X is its networking capability, which plays a central point in administration of many desktops and can also assist in the deployment of a thin-client computing environment. The capability to launch applications on remote desktops and also standardize installations highlight the versatility of this powerful application.

More recent versions of X have also included support for shaped windows (that is, nonrectangular), graphical login managers (also known as display managers), and compressed fonts. Each release of X brings more features designed to enhance the user experience, including being able to customize how X client applications appear, right down to buttons and windows. Most office and home environments run Linux and X on their local machines. The more-enlightened companies and users harness the power of the networking features of X, enabling thin-client environments and allowing the use of customized desktops designed specifically for that company. Having applications launch from a single location makes the lives of system administrators a lot easier because they have to work on only one machine, not several.
