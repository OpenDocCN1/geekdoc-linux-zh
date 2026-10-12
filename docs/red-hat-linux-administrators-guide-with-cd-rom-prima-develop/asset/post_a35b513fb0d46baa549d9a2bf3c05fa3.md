
as used in that cartoon. Thus the themes that KDE offers are similar to those used on both Windows and Apple operating systems, except that KDE makes it easier for the average user to choose them.

Themes for whatever window manager you are using are available on the Internet. One of the most popular sites for the exchange and creation of new themes for nearly all window managers is [http://www.themes.org/](http://www.themes.org/). You may either download or contribute your own design to the database for others to use. The site provides explicit instructions for designing your own theme and for sharing the information. Many themes come preinstalled with the manager, but you can add hundreds of themes later from the Internet as they become available.

To add a theme to the KDE desktop, locate the KDE Control Center under the KDE Start button. Under the second or Desktop item, look for the Theme Manager item. KDE installs a few themes by default but you can quickly add more. Sites such as [http://www.themes.org/](http://www.themes.org/) or one of the themes.org sub-domains, [http://kde.themes.org/](http://kde.themes.org/), host a wide range of themes for all desktops. Simply download one that looks interesting, save it to a temporary location or one that you can use for storing additional themes, and then click the Add... button under the Theme Manager. You may also change existing themes by giving them a new name or even create your own theme. The same page offers detailed instruction for theming both the KDE desktop and nearly all other window managers. Under the page of your choice, choose the Creating themes link to see how a sample theme is made. Naturally, the site promoters encourage Linux for all users and suggest using the GIMP to create each image within the customized theme.

As with the themes available under the Windows operating system, the user can customize a multitude of KDE items to suit. You can change or configure a theme's colors, wallpaper, panel, sounds, icons, window border, window titlebar, window gimmick, window button layout, file manager, and console. Whether you create your own theme or choose to use an existing one, KDE and other managers enable you to customize your interface to your liking, rather than restricting you to an appearance determined by a commercial developer.

## Discussing the KDE Packages

Because it requires few programs, KDE installs quickly and easily on any Linux box, no matter the distribution. Red Hat has provided as much support for this environment as it has for GNOME, so you can either install KDE initially or upgrade later using RPMs from the Red Hat site. KDE also provides Red Hat-specific RPMs from its own FTP site, [ftp://ftp.kde.org/](ftp://ftp.kde.org/).

As with any program, there are two major methods of installing KDE: source or RPMs. For many, compiling the source from scratch is the only way to install a manifold program such as KDE. Source code is usually released prior to the RPMs, so to ensure that you have the very latest updates, patches, and features, installing from source is the optimal method. Just as GNOME requires the GTK libraries, KDE first mandates that you install the Qt libraries. These are available from the main Qt site at [http://www.troll.no/](http://www.troll.no/) or from the main KDE site as well. They are also available in either source or RPM format. Be sure to read their instructions before attempting any sort of install. There is still some discrepancy between installing the 1.x and 2.x versions of Qt. By the time this book is in print, the latest release of KDE will have adopted the 2.x libraries as its standard.

If you are using RPMs to upgrade, you install the Qt libraries by issuing the simple RPM command in the same directory that the RPM libraries are located:

```bash
rpm -Uvh *.rpm
```

You can find all the documentation needed for compiling and installing at the main KDE home page, [http://www.kde.org/](http://www.kde.org/). To avoid increasing the already congested traffic at this site, try one of the many mirrored sites. These locations carry all the same source code, documentation, and information as the main KDE site. Using a mirror site will most likely also increase your download speed, which, considering the size of many of these files downloaded via a modem, can be quite tedious.

The documentation includes explicit instructions on how to compile and install each program on your hard drive. Generally you can install as many as 10 packages, although only two are required and a third is recommended. The others merely complement the core KDE files with a wide assortment of utilities. Sequence is also important in successfully installing the programs. Here is the recommended order as shown on the main KDE installation page:

- **kdesupport** (recommended). This package contains support libraries that have not been written as part of the KDE project, but which are needed nevertheless. If the libraries in this package (libgif, libjpeg, libmime, libau, and libgdbm) are already installed on your system, you may not need to install kdesupport. You should probably install it if only to standardize on the release.
- **kdelibs** (required). This package contains shared libraries that all KDE applications need.
- **kdebase** (required). This package contains the base applications that form the core of the K Desktop Environment: the window manager, the terminal emulator, the control center, the file manager, and the panel.
- **kdegames** (optional). This package includes few games such as *Mabjongg*, *Snake*, *Asteroids*, and *Tetris*, to name a few.
- **kdegraphics** (optional). This package includes various graphics-related programs such as PostScript Previewer, DVI Previewer, and a drawing program.
- **kdetools** (optional). This package includes various desktop tools, including a calculator, an editor, and other nifty utilities also found on a default Red Hat install but using the Qt libraries and optimized for KDE.
- **kdemultimedia** (optional). This package contains multimedia applications such as a CD player, a mixer, and an MP3 player.
- **kdenetwork** (optional). This package includes Internet applications. Currently the package contains the mail program, the news reader, and several other network-related programs.
- **kdeadmin** (optional). This collection of system administration programs includes the user manager and the System V run-level editor among others.
- **kdetoys** (optional). This package includes toys.
- **korganizer** (optional). This package completes your desktop with an organizer.

You are not required to install the optional programs in this order, but you might experience problems if you do not install the first three programs—kdesupport, kdelibs, and kdebase—correctly or in the order indicated in this list. After you have installed the packages and verified that they defaulted to the /opt/kde directory (you may choose another directory in which to install KDE, but it’s best to comply with the program defaults), you may then edit the .xinitrc file in your home directory so that KDE starts automatically when you boot into the X Window system. If there is no .xinitrc file in your home directory, create one at the terminal window. Using your favorite text editor, such as vi, pico, joe or jed, add the command startkde to your .xinitrc file. This command authorizes KDE to be the default X interface on subsequent bootups as well.

If you are booting into run level 5 of the default Red Hat desktop or you are bypassing the command line and logging in at the GUI, you can choose KDE as your default window manager. Otherwise, after logging in to GNOME manually, you may reconfigure your default environment to KDE by executing the switchdesk command. This command enables you to choose between GNOME, KDE, or the most basic GUI.

The next time you enter startx at the command line, KDE will automatically create additional directories in your home directory where it will store information. The latest version of Red Hat creates a Desktop directory automatically in case you choose KDE as your default interface. You may bypass this function by removing the Desktop directory from the /etc/skel/ directory. Subsequent users will not receive a KDE directory unless they manually choose KDE as their startup.

KDE provides a detailed help manual to help you learn more about its functions and accessories. For the purposes of this chapter, it is sufficient to cover some of

![Figure 12.3](img/a0884097af3186d9b4f616aaa3f065b0_438_0.png)

*Figure 12.3: A themed desktop under the KDE environment.*
