
# Chapter 8 ♦ The X Window System

- The k3b application is a front end to the various programs needed for creating and burning ISO images to CD or DVD.
- The kooka application is well featured for controlling a scanner.

## GNOME

The other desktop environment for Linux GNOME. There is something of a tradition of dichotomies in this world: the disagreement between the devotees of vi and emacs. In the area of scripting languages there is a similar split between the followers of Perl and those who use Python. On the desktop, it is KDE versus GNOME.

As noted, GNOME began as a reaction against KDE and the license of the Qt toolkit. The Qt used in KDE is acceptable to all. It is worth noting that there is a significant difference in that GNOME applications can be (and) compiled and offered on the Windows platforms; the Qt license does not allow the same to be done with KDE applications, although it is possible in principle.

Traditionally, KDE was the default on SUSE. SUSE GNOME packages tended to be well looked after, and well integrated into the rest of the system. There was also a tendency for them to be somewhat up-to-date than the KDE versions. On one occasion the timing of a SUSE release was calculated to be exactly in time to carry a large KDE release.

As KDE, GNOME attempts to provide an entire desktop environment in which compliant applications can cooperate in drag-and-drop, copy-paste, and other tasks. Again, with KDE, this means significant costs in overhead before any programs are actually run. Discussions around about which approach is technically better and about which environment has a better look and feel and better programs.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_253_0.png)

The free desktop at www.edesktop.org focuses on interoperability between different desktop environments for the X Window System. The project's goal is to provide a common infrastructure that KDE, GNOME, and others can agree upon and bound. Upon the founding of the project the widely shared feeling that the differences between GNOME and KDE were likely to hinder the adoption of Linux as a desktop system by businesses.

SUSE provides an up-to-date version of GNOME in order to support the latest and greatest GNOME applications. Some of the key GNOME applications are the Nautilus mail client, the Evolution mail client, the GIMP graphics package, the AbiWord word processor, the Gnumeric spreadsheet, the Inkscape vector graphics package, and (slightly tangentially as they are not strictly part of the project) the Mozilla browser and popular derivatives such as Firefox.

Parallel to the official SUSE GNOME packages is the Xian GNOME (Ximian Desktop 2) distribution, a version of which is available for SUSE. The only problem at present with using this version is that it means you will have to be very careful about what online updates you perform.

Another set of GNOME packages for SUSE systems is available from www.user-local-bin.org/. These packages are produced by a former SUSE employee in the UK and are very popular.

In many ways, the user’s point of view, there is little difference when choosing KDE and GNOME (see Figure 8-4).

However, some differences do exist and couple of notable ones as follows:

- One difference that you will immediately notice is that default KDE is a oneclick interface: Clicking an icon once launches the application or action. In most cases, it is intuitive and corresponds well with the one-click nature of links, but it is still difficult for the user coming from Windows. It can cause problems when you need to select an item and then do something with it. In most cases a right-click enables you to do what you want. GNOME’s double-click default is perhaps easier for Windows refugees (though KDE can be reconfigured to use double-clicks, as well).

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_254_0.png)

Figure 8-4: A new user’s default GNOME desktop

✦ Another key difference between GNOME and KDE is that technically GNOME does not include its own window manager; it requires a GNOME-compliant window manager. These days that means the metacity window manager, although in the past GNOME was normally used with the sawfish window manager. KDE can also use other window managers, although it uses its own, kwin.

## Nautilus

Nautilus should be thought of as a file manager. It is capable of rendering web pages, but it does this by calling an embedded external viewer, and by default out of the box, it views the HTML source rather than the rendered page.

As a file manager, Nautilus is attractive. By default, it shows files in an intuitive and friendly way; with Conqueror, image files and other types are shown as thumbnails or miniature copies of themselves. Selecting and copying files using the copy-paste or drag-and-drop features works, but there is no splitting the main window. If you want to drag files from one directory to another, you need to have each directory in a separate window.

## Epiphany

By default, the GNOME desktop web browser in SUSE is Epiphany, one of down browsers based on Mozilla (another is Galen). It should be considered a disadvantage that, unlike in KDE, in GNOME it is not natural to “do everything in one place." You can, browse the file system with Epiphany, but you can not use it to move files around.

## Evolution

Evolution is the GNOME mail client; people who use it tend to be very fond of it. It is deliberately similar in look and feel to Microsoft Outlook and has integrated ending capabilities. Xianian's Evolution Connector (a piece of software allowing Evolution to connect to a Microsoft Exchange server and exchange calendar information) has recently been released as open source by Novell.

## Gnucash

Gnucash is a personal finance application with similar features to some of the proprietary applications in this field.

## AbiWord

AbiWord is a word processor with many advanced features. However, as in the case of kword, mentioned previously, poor importing of Microsoft Word files means that it does not compare well with OpenOffice.org.

## Gnumeric

Gnumeric is an impressive spreadsheet program. Similar considerations regarding importing other file types that we mentioned when discussing AbiWord apply, however. OpenOffice.org certainly seems to have the edge in that regard, although as a standalone spreadsheet, Gnumeric compares quite well in terms of features with the OpenOffice.org spreadsheet and Microsoft Excel. It also offers some scientific functions, as its Solver for linear equations and its Simulation and Statistical Analysis capabilities, that are not currently available in other spreadsheet applications.

> Of course, there is nothing to stop you from running applications designed for one of the desktops without the other. The design of the menus tends to push you toward one of set programs rather than the other. In addition, if you are going to run Conquer, for example, within a GNOME environment, it will start a fairly large proportion of the KDE infrastructure in the background simply to support it. Integration between the two environments has improved, and each finds displays programs from the other in its menu structure.

## Other Window Managers

If you decide not to either KDE or GNOME, a variety of X window managers are available. Essentially, your choice is about balancing beauty against simplicity.

- If resources are limited, one of the minimal window managers may suit you. Also, if you are in the habit of starting everything from the command line, then complex menus and icons may not be so useful to you. At the very minimal end of the spectrum, TWM, and Fluxbox (discussed later in this chapter) provide an environment where you can start an xterm and everything else from there. Apart from the ability to move and minimize windows, there is not a great deal of other functionality.
- On the other hand, a window manager such as X offers complex menus, a great deal of configurability, and a lot of eye candy, but uses a good deal of resource and the nice built-in file management capabilities of GNOME and KDE.

Window managers such as IceWM and Blackbox fall somewhere between the two extremes. In general, if you use one of these window managers you are going to find yourself spending a fair amount of time doing configuration to get the look and the way you want and the menus the way you want: At least some of this work will be spent editing text files by hand.
