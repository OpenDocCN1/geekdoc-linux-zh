# Window Manager

The window manager determines how the GUI looks on your monitor. There are several different kinds of window managers available including GNOME, KDE, Afterstep, Window Maker, fvwm, Blackbox, and Enlightenment.

The two most common default window managers are GNOME and KDE. The GNOME window manager is built from the GTK+ widget library. The KDE window manager is built from the Quicktime (Qt) widget library.

# Applications

For the most part, GUI applications, such as Netscape Communicator and WordPerfect, work with but are not part of the X Window architecture. Nevertheless, GUI applications also store user-specific configuration files. You may already have some hidden application configuration files in your home directory.

The GNOME and KDE packages include applications such as office suites.

# X Window Configuration Utilities

Editing the XF86Config file can be a difficult process for all but the most skilled administrators. There are a number of good tools available to help you configure this file. Although some of these tools are graphical, they do not suffer from the perceived flaws of other Linux GUI utilities. In other words, they are reliable. For the most part, they include all of the features that most administrators need to configure their systems.

Some of these utilities can even help you install or revise settings for your keyboard and mouse.

![](bbox=[0.12, 0.9, 0.22, 0.97])

> Before you start any of these utilities, back up your X Server configuration file, which is normally /etc/X11/XF86Config.

# SuperProbe

The SuperProbe utility is a text command that detects key parts of your video controller, including the chipset on the card and the data converter. Most importantly, it identifies an appropriate X Server for you. If you want to try to use this utility, close all currently running programs first because SuperProbe can make Linux "hang" or stop working on your computer.