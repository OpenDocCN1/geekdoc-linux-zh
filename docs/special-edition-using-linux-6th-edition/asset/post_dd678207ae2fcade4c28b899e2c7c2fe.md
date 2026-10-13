
at more novice users (though advanced users often find them incredibly useful). Often, a desktop user can do all her work without ever invoking a command line.

## CDE

Several UNIX producers, including Hewlett-Packard, IBM, Novell, and Sun Microsystems, have worked together to produce CDE, the *Common Desktop Environment*. This environment is based on earlier UNIX desktops such as HP-VUE. Although CDE provides a very configurable interface, including drag-and-drop, session management, and a powerful panel, it lacks several features that other desktops provide:

- Files and shortcuts cannot be placed directly on the desktop.
- Much of the configuration must be handled through complex configuration files instead of graphical dialogs.
- Whereas CDE has been ported to Linux, it is not Open Source software, nor is it free.

## KDE

In 1996, Matthias Ettrich began work on KDE, which is shown in Figure 2.1. Built on top of the Qt toolkit from Trolltech, KDE provided a friendly, powerful, and highly configurable environment targeted at the novice user. Billed as “UNIX for the Desktop,” KDE represented one of the first major steps toward Linux for the mass market.

**Figure 2.1**  
The KDE desktop provides a friendly interface similar to the Macintosh, Windows 98, and BeOS interfaces.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_42_0.png)

> **Tip**  
> The “K” in KDE doesn’t stand for anything. KDE is simply the K Desktop Environment.

KDE provides many features, some of which will be covered later in “Common Desktop Features,” and still more of which will be covered in Chapter 3, “KDE.” The most significant, however, is a consistent desktop metaphor, similar to the one first introduced by MacOS. Also like MacOS, KDE applications follow a consistent style guide, which means that all KDE applications tend to work similarly. For example, nearly all KDE applications have a File menu as the first entry on their menu bar and a Help menu as the last entry.

## GNOME

The KDE project’s basis on the Qt toolkit caused much controversy in its early days. The original Qt license was not Open Source (as defined by the Open Source Initiative, or OSI), and there was some concern that Trolltech might someday go out of business or modify its license in such a way that KDE could no longer be free. This concern was generally alleviated with the creation of the KDE Free Qt Foundation, which ensures that if Trolltech ever stops developing Qt Free Edition, it will be released under the BSD Open Source license. Furthermore, should Trolltech (or their successors) ever want to change Qt Free Edition’s license, it must be approved by the Foundation, of which KDE developers have a majority voting interest. Trolltech went even further, first by releasing Qt Free Edition under the Qt Public License (QPL), which was certified as an Open Source license by the OSI, and finally by releasing Qt under the GPL.

These historical concerns led to the creation of the GNOME project. The GNOME project set out to create a desktop, which is shown in Figure 2.2, and which was fully under the GPL license.

**Figure 2.2**  
GNOME is the first fully Open Source desktop for UNIX.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_43_0.png)

Where KDE has a fairly strict style guide, ensuring that its applications conform to a consistent look and feel, GNOME thrives on individual creativity. Although this has allowed GNOME to often leap ahead in configurability and features, it has also generally reduced the integration of its parts. This has changed greatly recently as GNOME has moved towards Bonobo, an interface for exchanging information between applications (similar to KParts in KDE or COM in Microsoft Windows).

Today, several commercial and non-profit organizations have arisen to help support GNOME. One of the most interesting is the GNOME Foundation. Founded in 2000, the GNOME Foundation is an advisory board that helps direct the development of GNOME. It is made up of the many volunteers who work on GNOME, but also includes numerous companies such as Compaq and Sun Microsystems.

Other corporate interests in GNOME include Helix Code and Eazel. Helix Code (www.helixcode.com) has put together a distribution of GNOME that is incredibly easy to install. This will be discussed more in Chapter 4, “GNOME.” Eazel (www.eazel.com) is working with GNOME and Helix Code to develop a very user-friendly desktop. Founded by some of the original Macintosh team, their goal is to bring Linux to the masses. Nautilus, their file and desktop manager, is expected to be the default desktop in GNOME 2.0.

As KDE and GNOME evolve, they begin to resemble each other more and more. Some of this is simply good ideas being passed back and forth, but some of this is very active. Efforts are underway currently to provide greater interoperability between the two desktops, allowing applications written for one to work more seamlessly with the other. Although it is unlikely that the two groups will ever merge, it seems very likely that users in the future will be freer to pick and choose the desktop and applications that suit them best.

## Xfce

GNOME and KDE are both very powerful desktops, but they also use a lot of memory and other system resources. Xfce offers much of the friendliness and configurability of the larger desktops at a fraction of the resources. Based on the same libraries as GNOME (GTK+) and offering an interface similar to CDE, Xfce works especially well with GNOME-based programs, but it also handles KDE applications without difficulty.

Xfce is ideal for those users who want a friendly interface on an underpowered machine, or simply for those users who prefer to save their resources for their applications instead of all the extra features of KDE or GNOME.

## Common Desktop Features

Although every desktop has its own special features, most desktops have many things in common. This is especially true in the Linux world as KDE and GNOME converge more and more. In this section we will cover the features that are common to most desktops and are more important to the user’s experience. For specific examples of these features, see Chapter 3, “KDE,” and Chapter 4, “GNOME.”

### DESKTOP

The most noticeable difference between a desktop environment and a window manager is the active nature of the desktop background. Whereas most window managers treat their background as simply an area that does not include a window, desktop environments allow you to use the background as if it were a globally available directory (in fact, it is usually implemented as a directory).

In a desktop environment, you can copy files, directories, shortcuts, and other objects directly to the desktop for quick access. These elements are available regardless of which virtual desktop you’re viewing (see the following section, “Pager,” for more information on virtual desktops). This is incredibly useful for providing quick access to your most used files and directories.

### SHORTCUTS

In an environment such as MacOS, where all applications know how to interact with the desktop, shortcuts are little more than symbolic links. In environments with a command-line heritage, such as Microsoft Windows and any UNIX desktop, shortcuts need much more information to be useful.

In KDE and GNOME, shortcuts are files that reference other files, applications, directories, or even desktop-specific features such as services or MIME types. They provide information about which icon to use, what application is used for this file, how to mount or unmount a device, the name of the application in numerous languages, and much more. Shortcuts can be placed on the desktop, the panel, a menu, or in other locations that the desktop uses for configuration.

### FILE ASSOCIATION

If you have ever clicked a file’s icon in MacOS or Microsoft Windows and had your machine automatically launch the correct application, you’ve used file associations. In Linux desktops, file associations match files to applications by their filenames or by fingerprints within the file. This allows files to display the correct icon and automatically launch the correct application.

### PANEL

Linux desktops generally have a panel that includes shortcut buttons, menus, and applets (small, embedded applications). Generally the panel is a bar across the bottom of your screen, but it can almost always be moved to one of the other edges of the screen.

The panel is one of the most useful parts of the desktop environment because it provides quick access to your most needed functions. Shortcuts quickly launch your most used applications, menus give access to lesser-used applications, applets such as a pager (see the following section), battery monitor, or clock provide extra functionality or monitoring. The panel is usually extremely configurable to your preferences and work style.
