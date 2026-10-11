
## Immediate Solutions

### Installing The X Server In Red Hat

Installing the X server is a multistep process in Red Hat. You have to determine which X server is appropriate for your video equipment and more. To install the full GUI if you did not do so during the initial installation process, do the following:

1. Log in as root.
2. Insert the first Red Hat CD-ROM into the CD-ROM drive.
3. Mount the CD-ROM with a statement such as the shortcut `mount /mnt/cdrom`, which is available in Red Hat.
4. Type `cd /mnt/cdrom/RedHat/RPMS` to change to the Red Hat Package Manager (RPM) directory.

> **TIP:** One feature of the bash shell that can save you much typing from here on is the Tab key. There is a technique called Tab completion that allows you to type a partial file name and, when you have typed enough to make it distinct from the others in the directory or path you are referring to, you can press Tab and the rest of the name automatically appears on the command line.

5. Type the following to install the X server components you need:
   `rpm -ivh XFree86-libs-3.3.6-20.i386.rpm XFree86-xfs-3.3.6-20.i386.rpm XFree86-3.3.6-20.i386.rpm`

> **NOTE:** It is important to use this exact order. The packages are listed in order of dependency, so that those packages requiring other packages are listed after the items they need.

6. Type `rpm -ivh gtk+-1.2.5-2.i386.rpm Xconfigurator-4.2.8-2.i386.rpm` to install the Red Hat tool that will help you configure your X server.
7. Type `Xconfigurator` to run the configuration tool. This instance is just a test, a quick cheat if you will. You are using it to see which specific X server you need to install. This choice will be revealed to you once you choose your video card.

**WARNING!** Be sure to choose the right video card entry, or if yours is not listed choose to enter a custom value. You can damage your equipment by being sloppy with video configuration.

8. When Xconfigurator exits with an error and lists which X server is not installed, note which server this is. You will find this server among the XFree86 files. For example, if the program exits complaining about XF86_SVGA, it wants the server XFree86-SVGA-3.3.6-20.i386.rpm.
9. Install the server. For example, `rpm -ivh XFree86-SVGA-3.3.6-20.i386.rpm`.
10. Run Xconfigurator again. This time, it should go through the entire configuration process.

**TIP:** It is a good idea to test the X server at this point in the Xconfigurator program. Otherwise, the X server may not be properly configured.

11. Once the program exits, your X server is installed and running. However, you still need to install GNOME or KDE—see the following section “Installing GNOME Or KDE In Red Hat.”

| Related solution | Found on page |
| :--- | :--- |
| Adding And Removing Media To The File System | 84 |

### Installing GNOME Or KDE In Red Hat

To install either the GNOME or KDE desktop environment in Red Hat Linux, begin with the following:

1. Log in as root.
2. Insert the first Red Hat CD-ROM into the CD-ROM drive.
3. Mount the CD-ROM with a statement such as the shortcut `mount /mnt/cdrom`, which is available in Red Hat.
4. Use `cd /mnt/cdrom/RedHat/RPMS` to change to the RPM directory.
5. Make sure you have already installed the X server, as discussed in the section “Installing The X Server In Red Hat.”
6. Proceed to the appropriate subsection to complete the installation.

### Installing GNOME

To install the GNOME desktop environment, do the following:

1. Type the following to install the pile of graphics and sound libraries necessary to run the Enlightenment window manager:

   ```bash
   rpm -ivh libtiff-3.5.4-5.i386.rpm libpng-1.0.5-3.i386.rpm libjpeg-6b-10.i386.rpm libungif-4.1.0-4.i386.rpm freetype-1.3.1-5.i386.rpm audiofile-0.1.9-3.i386.rpm esound-0.2.17-2.i386.rpm libgr-2.0.13-23.i386.rpm libgr-progs-2.0.13-23.i386.rpm imlib-1.9.7-3.i386.rpm fllib-0.4.10.i386.rpm
   ```

   > **TIP:** One feature of the bash shell that can save you much typing from here on is the Tab key. There is a technique called Tab completion that allows you to type a partial file name and, when you have typed enough to make it distinct from the others in the directory or path you are referring to, you can press Tab and the rest of the name automatically appears on the command line.

2. Type `rpm -ivh enlightenment-0.15.5-48.i386.rpm` to install the Enlightenment window manager.
3. Type the following to install the many graphics and sound libraries necessary for the GNOME desktop environment:

   ```bash
   rpm -ivh xpm-3.4k-2.i386.rpm ORBit-0.5.0-3.i386.rpm gnome-audio-1.0.0-8.noarch.rpm gnome-libs-1.0.55-12.i386.rpm libgtop-1.0.6-1.i386.rpm libghttp-1.0.4-1.i386.rpm libxml-1.8.6-2.i386.rpm libglade-0.11-1.i386.rpm xloadimage-4.1-13.i386.rpm xsscreensaver-3.23-2.i386.rpm control-center-1.0.51-3.i386.rpm MagIcev-0.2.7-1.i386.rpm
   ```

4. Type `rpm -ivh gnome-ore-1.0.55-12.i386.rpm` to install GNOME itself.
5. Often from here you would create your own X initialization files, but Red Hat provides a package to start this process for you. Use `rpm -ivh xinitrc-2.9-1.i386.rpm` to install it.
6. There are a number of other GNOME packages you may want to install as well. These items are listed in Table 6.1.

### Installing KDE

To install the KDE desktop environment, do the following:

1. Type the following to install the many graphics and sound libraries necessary for KDE:

   ```bash
   rpm -ivh libungif-4.1.0-4.i386.rpm libjpeg-6b-10.i386.rpm libpng-1.0.5-3.i386.rpm qt-2.1.0-4.i386.rpm qtlx-1.45-3.i386.rpm kdesupport-1.1.2-12.i386.rpm compat-libs-5.2-2.i386.rpm xpm-3.4k-2.i386.rpm kdelibs-1.1.2-15.i386.rpm libtiff-3.5.4-5.i386.rpm
   ```

| Package | Purpose |
| :--- | :--- |
| enlightenment-conf-0.15-9.i386.rpm | The configuration component for the Enlightenment window manager |
| gnome-games-1.0.51-4.i386.rpm | A set of games |
| gnome-linuxconf-0.25-2.i386.rpm | The GNOME Linux configuration tool; highly recommended |
| gnome-media-1.0.51-2.i386.rpm | A set of multimedia tools |
| gnome-objc-1.0.2-6.i386.rpm | Objective C GNOME libraries; highly recommended |
| gnome-pim-1.0.5-1.i386.rpm | The GNOME Personal Information Manager; contains a calendar, to do list, and contact list management software |
| gnome-users-guide-1.0.72-1.noarch.rpm | A reference for users trying to find their way through GNOME |
| gnome-utils-1.0.50-4.i386.rpm | A variety of utilities for GNOME, such as a calculator |

> **TIP:** One feature of the bash shell that can save you much typing from here on is the Tab key. There is a technique called Tab completion that allows you to type a partial file name and, when you have typed enough to make it distinct from the others in the directory or path you are referring to, you can press Tab and the rest of the name automatically appears on the command line.

2. Type `rpm -ivh kdebase-1.1.2-33.i386.rpm` to install KDE itself.
3. Often from here you would create your own X initialization files, but Red Hat provides a package to start this process for you. Type `rpm -ivh xinitre-2.9.1.noarch.i386.rpm` to install it.
4. There are a number of other KDE packages you may want to install as well. These items are listed in Table 6.2.

| Package | Purpose |
| :--- | :--- |
| kdeadmin-1.1.2-6.i386.rpm | KDE system administration tools |
| kdebase-lowcolor-icons-1.1.2-33.i386.rpm | KDE icons that work best with an 8-bit video card |
| kdegames-1.1.2-3.i386.rpm | A set of games |
| kdegraphics-1.1.2-3.i386.rpm | A set of graphics tools |
| kdemultimedia-1.1.2-7.i386.rpm | A set of multimedia tools |
| kdenetwork-1.1.2-13.i386.rpm | A set of networking tools; recommended |
| kdetoys-1.1.2-3.i386.rpm | A set of amusements for KDE that do not quite qualify as games |
| kdeutils-1.1.2-4.i386.rpm | A variety of utilities for KDE, such as a calculator |

## Finding GUI Components Online

If you want to locate additional window managers, display managers, or themes—unified looks created by various people—you can do so online. To locate them, do one or more of the following:

- Go directly to the GNOME ([www.gnome.org](http://www.gnome.org)) or KDE ([www.kde.org](http://www.kde.org)) Web site.
- Go directly to the sites listed in the In Depth section “Window Managers.”
- Go to [www.themes.org](http://www.themes.org) to peruse a long list of available options, including various graphically unified themes that you can apply to GNOME or KDE.

Once you find an item you would like to try, download it to your system and save it in a separate directory from the main GUI tools. Put it where you can easily tell what items you can erase at a later date without worry, such as in a subdirectory in your home directory.

Some new GUI elements are actually included on the Red Hat CD-ROM. In these cases, you can install the RPMs and not worry about where the files are placed, because you can uninstall the RPMs later.

## Adding A Window Manager

When you want to add a new window manager and try it out, you need to find a way to tell the GUI where to find it and what it is. GNOME and KDE each offer tools that allow you to do this quickly and easily. You can change such settings directly at the command line as well.

### Adding A Window Manager In GNOME

If you want to try a new window manager in GNOME and have already downloaded it, do the following:

1. Click on the Toolbox icon to open the GNOME Control Center.
2. Click on the Window Manager under the Desktop tree to open the Window Manager dialog box, shown in Figure 6.1.
3. Click on the Add button to open the Add New Window Manager dialog box.
4. In the Name field, type in the window manager’s name. This item exists only for your reference, so give it the name of the file or something else that reminds you of it.
