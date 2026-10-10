
color depths, and your XF86Config file's Screen section should have Display sub-section entries for each color depth. For example:

```
Section "Screen"
Driver "svga"
Device "My Video Card"
Monitor "LCD Panel 1024x768"
Subsection "Display"
Depth 8
Modes "1024x768" "800x600" "640x480"
EndSubsection
Subsection "Display"
Depth 16
Modes "1024x768" "800x600" "640x480"
EndSubsection
Subsection "Display"
Depth 24
Modes "1024x768" "800x600" "640x480"
EndSubsection
EndSection
```

These entries show configurations for color depths of 8-bit planes (256 colors), 16 (thousands of colors), and 24 (millions of colors), with different resolutions for each color depth. Use startx with its bpp (bit plane) option to start an X11 session with millions of colors:

```
# startx -- -bpp 24
```

After you press Enter, X will start. The X server determines whether the notebook can support a resolution of 1024×768 with millions of colors. If not, the next resolution is tried, and so on until one is found that works. Ideally, you should know the limitations of your notebook's display for each color depth and then craft your system's XF86Config file to support each resolution and color depth. Some notebooks, such as Sony's 505TX and TR series, can also use special option entries in XF86Config's Device section to support these modes. For example:

```
Option "lcd_center"
Option "no_stretch"
```

These entries, as detailed in the file README.neo (505s use a NeoMagic graphics chipset) under the /usr/X11R6/lib/X11/doc directory, disable stretching of lower-resolution modes and center the lower-resolution screen on the notebook's LCD. This allows for better font display when using various combinations of resolution and high color depth. This is another good reason to read documentation for your notebook's graphics chipset. Using different options can mean the difference between distortion and a readable display!

# Choosing a Window Manager

X11 provides various servers and clients for your X session. Much of the magic of moveable windows, scroll bars, drag-and-drop, buttons, dialogs, icons, and other features of the modern graphical interface to Linux occurs because of a special X11 client known as a *window manager*. There are literally hundreds of window managers for X11, thanks to the efforts of thousands of programmers around the world. The ability to choose a window manager for your needs is yet another good reason to use Linux, X11, and Open Source software, and to avoid proprietary systems that lock you into using an interface that might or might not work well for you.

Choosing a window manager for your notebook involves a number of considerations:

- **RAM usage.** How much memory does the window manager require and use?
- **CPU resources.** How much of your CPU's horsepower is needed when running the window manager?
- **Hard drive space.** How big is the window manager and any associated software?
- **Associated clients.** How many clients are included with the window manager, work well with it, or take advantage of any of its special features?
- **Features.** What kinds of special features, such as drag-and-drop, icon docks, menus, or panels, are supported?
- **Ease of use.** How easy is it to use, configure, and maintain the window manager and its associated software?
- **Security.** Does the window manager have any security flaws?
- **Support.** How many people are working on this window manager, is it included with most major Linux distributions, and are new clients being developed for it?
- **"Coolness" factor.** Do other mobile Linux X11 junkies drool with envy when they see your notebook's display?

XFree86 comes with one window manager—the Tab Window manager (*twm*)—but most Linux distributions now include the GNOME-enabled Enlightenment window manager and the K Desktop Environment. Table 9.3 lists a number of the more popular window managers available for X11 and Linux.

| Window Manager | Description | URL |
|---|---|---|
| AfterStep | Looks and feels like NEXTSTEP | http://www.afterstep.org |
| amwm | Amiga Window Manager | http://www.lysator.liu.se/~marcus/amwm.html |
| blackbox | Minimalistic window manager | http://blackbox.alug.org |
| CDE | Common Desktop Environment (commercial software) | http://opengroup.org |
| ctwm | Based on twm with extensions | http://brudg.ctlr.c-l.iiu.se/~dl/ctwm |
| Enlightenment | Complex and capable; GNOME-aware | http://www.enlightenment.org |
| fwm | Based on twm with numerous improvements; version 2 is also available | http://www.fwm.org |
| fwm95 | Based on fwm2 | http://www.foxproject.org/xclass/fwm95.html |
| IceWM | Highly configurable | http://icewm.sourceforge.net |
| KDE | The K Desktop Environment; very popular | http://www.kde.org |
| lwm | Lightweight Window Manager; no features | http://users.ch.genedata.com/~enh/lwm/ |
| mlwvm | Makes your desktop look like a Mac | http://www2u.biglobe.ne.jp/~y-miyata/mlwvm.html |
| mwm | Motif window manager (also included with the free LessTif distribution) | http://www.openmck.org and http://www.lesstif.org |
| olvwm | OpenLook window manager; based on Sun Microsystems' code | ftp://ftp.x.org/R5contrib/ |
| sawmill | Features a Lisp-based configuration scripting language | http://sawmill.sourceforge.net |
| scwm | Scheme Constraints Window Manager; features scripting | http://scwm.mit.edu/ |
| twm | Included with XFree86; minimalist window management | http://www.x.org |
| vtwm | Based on twm, but includes virtual desktops | http://www.visi.com/~hawked/vtwm.html |
| WindowMaker | Emulates the NeXt interface | http://www.windowmaker.org |
| wm2 | Extremely small and compact | http://www.all-day-breakfast.com/wm2/ |
| wmx | wm2 variant, also extremely small and compact | http://www.all-day-breakfast.com/wmx/ |
| XFCE | XFce Desktop Environment; features a CDE-like panel | http://www.xfce.org |

Note that Table 9.3 does not list GNOME. This is because GNOME is not a window manager, but a set of libraries and clients used with GNOME-aware window managers, such as Enlightenment. Using GNOME or KDE on your notebook requires hundreds of additional megabytes of storage space but provides a modern graphical interface for your X11 sessions.

# Maximizing Your Screen Real Estate

One window manager feature you can take advantage of during your X11 sessions is the use of an additional display screen, or *virtual desktop*. Not all window managers (and especially not those designed for minimalists) provide this feature. Legacy X11 window managers, such as *fvwm* and *olvwm*, provide a hint about this feature in their name (the *v*). When you use a window manager that features a virtual desktop, you'll generally find a small window, dialog box, or set of buttons known as a *pager* that provides navigation to each screen.

Using virtual desktops is a great way to keep work areas organized and perhaps sorted by function. For example, you can conduct your word processing on one desktop, electronic mail in another window, Web browsing in a third, and so on. Figure 9.3 shows a typical pager supporting four virtual desktops, with applications running in two of the desktops.

To navigate to a different desktop, click one of the squares. Your entire display will change to reflect the new desktop. Nearly all window managers allow you to configure the number of virtual desktops used during your X11 sessions. Legacy desktops, such as *fvwm*, use a text file, known as a *resource file*, to contain settings that can be changed only between X sessions. Newer X11 window managers and desktop environments, such as KDE, provide graphical interface configuration tools.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_253_0.png)

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_254_0.png)

> Figure 9.4 KDE's panel configuration tool can be used to change a number of panel settings, including the number of virtual desktop buttons available on the panel's pager.

to allow changes during your X session. For example, KDE's kpanel configuration tool, shown in Figure 9.4, allows you to change the number of virtual desktops from two to eight.

As with running multiple X sessions, running numerous applications in different virtual consoles might eat up your system's resources, but you'll be able to quickly switch between applications and keep your work organized on different displays.

# Working with an External Monitor

If you really need extra screen real estate or you want to use a larger display, you can hook your notebook up to an external monitor (as long as your notebook or replicator port provides an external video out port). You might need to make a change in your notebook's BIOS during a reboot in order to enable the use of an external display. You might also need to toggle the display of your notebook's LCD on or off by using a special Fn key combination on your laptop's keyboard.

If you can display the Linux text-only console on an external monitor, but not your X11 session, check to see if your XF86Config needs to be edited to include special
