
## Set Target Partitions/Filesystems

This module is used to configure the target partitions for the installation. You use it to tell YaST where to install the packages on your hard disk. You also can use it to configure the mount points for the various partitions on your system. This module is self-explanatory and very easy to use (see Figure C.12).

FIGURE C.12
Setting the target partitions and mount points using YaST.

![](img/659f91d9da7b29976c0625e2e9628511_689_0.png)

## Installing to a Directory

This module enables you to set a directory to be used by YaST as the installation destination. You can install SuSE Linux on another partition or hard disk while your system is still running. Just enter the path to the directory to which you want to install (see Figure C.13).

FIGURE C.13
Installing to a directory.

![](img/659f91d9da7b29976c0625e2e9628511_689_1.png)

## Choose/Install Packages

The Choose/Install Packages section is one of the most important sections in YaST; it is the package manipulation center. You frequently will come here to install new packages, remove unwanted packages, and so on. The module is menu driven, as you can see in Figure C.14.

The following lists the items in this menu:

- Load configuration—This menu item enables you to load one of the preset package configurations for quick installations, so you can skip the process of manually choosing the packages.
- Save configuration—If you have manually selected some packages, you can save this configuration so you can load it up later using the Load configuration option.
- Change/create configuration—This is where you browse all the packages that come with SuSE Linux to select which ones you want to install and which you want to remove from your system.
- Check dependencies of packages—Some packages in SuSE Linux depend on the presence of other packages for proper functioning. This menu item will show you whether you have any packages that are missing some dependencies. You can have it resolve these dependencies for you by installing the required packages.
- What if—You can use this menu item to have YaST tell you what is going to happen if you proceed to install with the current configuration. This enables you to know what is going to change in your system so you can then prevent any unwanted deletions or additions.
- Start installation—After you are finished configuring the packages, you can install them using this option. YaST then starts installing the packages to your hard disk.
- Index of all series and packages—This option shows you an index of all the packages and the series to which they belong.
- Package information—You can use this module to search all the packages using patterns, enabling you to locate a package when you don’t know its actual name.
- Install packages—This menu item launches a general package installation module. You can use it to install packages from a variety of different sources, not just the SuSE Linux CDs. This is very useful if you have downloaded some packages and want to install them.

# FIGURE C.14

The package configuration and installation menu.

![](img/659f91d9da7b29976c0625e2e9628511_690_0.png)

- Delete packages—This menu item launches a general package management module. You can use it to delete any of the packages on your system regardless of where they came from.
- Main menu—This menu item takes you back to the main menu.

Let's take a closer look at the important modules.

## Change/Create Configuration

You will probably use this module frequently in SuSE Linux. In most of the chapters in this book, you have had to install certain packages from the SuSE distribution. This is the module you use to install those packages.

YaST shows you a list of all the series found on your SuSE distribution (see Figure C.15). Packages are ordered according to series; for example, the Apache Web server package is found under series n (network). To select a package, highlight the series to which it belongs and press Enter. Packages can have one of the following five states:

- [ ]—The package is not installed on your system.
- [i]—The package is already installed on your system.
- [X]—The package is now selected for installation on the system.
- [R]—The package is already installed but will be reinstalled.
- [d]—The package is selected for removal.

FIGURE C.15
Changing the configuration of packages.

![](img/659f91d9da7b29976c0625e2e9628511_691_0.png)

You can change the state of a package by pressing the space bar to cycle through all five states.

To exit from a series, press F10 (the same applies if you want to exit the whole module). Next, you must install the packages by selecting the Start installation option from the main menu and pressing Enter.

## Install Packages

The Install Packages module is a general package installer. You can use it to install packages from a variety of different sources, including your source medium. The first thing you must do is to tell the module where to find the packages you want to install by selecting the correct source from the Source field (see Figure C.16).

# FIGURE C.16
General package installation.

![](img/659f91d9da7b29976c0625e2e9628511_692_0.png)

When you select the source of the packages, which can be a directory, the source medium, FTP, or a floppy disk, you will see a list of all the available packages. A common scenario for this is that you downloaded a few packages in RPM format and want to install them. Say you downloaded them in a directory called /tmp/downloads. You would tell YaST that your source is a directory and then enter /tmp/downloads as the path of that directory. YaST then would scan the directory and list all the packages in it. The packages can have one of the following four states:

- [ ]—The package is not installed on your system.
- [I]—The package is already installed on your system.
- [X]—The package is now selected for installation on the system.
- [o]—Another version of the package is installed on your system.

When you are finished selecting the packages you want to install, press F10 to install them on your system.

## Delete Packages

This menu item launches a general package management module. You can use it to delete any of the packages on your system regardless of where they came from. This module will show you a lengthy list of all the installed packages on your system (see Figure C.17). To delete a package, mark it with an X by pressing the spacebar. Press F10 to delete the selected package(s).

# FIGURE C.17
General deletion of packages.

![](img/659f91d9da7b29976c0625e2e9628511_693_0.png)

## System Administration

The System Administration menu item branches out to another submenu. This submenu contains all the modules relevant to administering your SuSE Linux system. The following is a brief list of these items (see Figure C.18):

- Integrate hardware into system—This item branches out into another submenu in which you can add hardware to and remove hardware from your system.
- Kernel and bootconfiguration—This item branches out into another submenu in which you can install new kernels to the system and all the system boot up-related configurations.
- Network configuration—This item branches out into another submenu in which you can configure your network.
- Configure Live-system—This item branches out into another submenu in which you can configure the SuSE Linux live system. The live system is a complete Linux system available in installed form on a CD.
- Login configuration—This is where you can configure how your SuSE Linux will handle logins. You can set SuSE Linux to start a graphical login manager or a console-based login manager.

# FIGURE C.18
The System Administration menu.

![](img/659f91d9da7b29976c0625e2e9628511_693_1.png)

- Settings of susem—This module enables you to configure the various window managers available on your system. You can use it to set the default window manager for your system.
- User administration—This module is used to manage all the users on the system. You can add, remove, and modify users here.
- Group administration—This module is used to manage all the groups on the system. You can add, remove, and modify groups here.
- Create backups—This module can be used to back up your system.
- Security settings—This item branches out into another submenu that contains your system’s security settings.
- Set the console font—You can set the console’s font in this module.
- Set time zone—You can set your time zone using this module.
- Configure XFree86—This module launches one of the three configuration programs that can be used to configure your X Window System.
- Configure GPM—This module configures your mouse for use in the console.
- Change configuration file—You can change many of the system variables using this module.

Let’s take a closer look at the submenus and the rest of the menu items.

## Integrate Hardware into System

You will use this menu whenever you want to configure your hardware. YaST cannot configure all of your hardware, but it does a good job with the common types. This menu has the following modules:

- Mouse configuration—This module configures your mouse (see Figure C.19). YaST asks you about your mouse type. Use the arrow keys to locate your mouse type and press Enter for SuSE to configure it. If your mouse is a serial mouse, YaST will prompt you for the COM port it uses.

FIGURE C.19
Configuring your mouse.

![](img/659f91d9da7b29976c0625e2e9628511_694_0.png)
