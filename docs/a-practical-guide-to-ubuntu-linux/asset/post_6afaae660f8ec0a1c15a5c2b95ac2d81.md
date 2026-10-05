
After the software is downloaded, while it is being installed, debconf asks if you want to use the gdm (GNOME) or kdm (KDE) display manager. Either one works with either desktop. One way to choose which display manager to use is to select the associated with the desktop you will be using most often.

Once KDE is installed, reboot the system. From the Login screen, follow the instructions on page 145 to display the Sessions drop-down list and select the session you want to run (GNOME or KDE).

## SETTING UP A DUAL-BOOT SYSTEM

A dual-boot system is one that can boot one of two (or more) operating systems. This section describes how to add Ubuntu to a system that can boot Windows, thereby creating a system that can boot Windows or Linux. You can use the technique for adding Ubuntu to a system that runs a different version or distribution. One issue in setting a dual-boot system is finding disk space for the new Ubuntu system. The next section discusses various ways to create the needed space.

## CREATING FREE SPACE ON A WINDOWS SYSTEM

Typically you install Linux in free space on a hard disk. To add Ubuntu Linux to a system, you must have enough free space on a hard disk that already holds Windows. There are several ways to provide or create this free space. The following paragraphs discuss these options in order from easiest to most difficult.

- Add new hard disk
Add another hard disk to the system and install Linux on the new disk, which contains only free space. This technique is very easy and clean but requires a new hard disk.

- Using free space
If there is sufficient free space on the Windows, you can install Linux there. This technique is the optimal choice, but there is rarely free space on an installed Windows system to use.

- Resize Windows partitions
Windows partitions typically occupy the entire disk, making resizing a Windows partition the most commonly used to free up space. Windows systems typically use NTFS, FAT32, and/or FAT16 filesystems. You can use the parted partition editor to resize an existing Windows partition to open free space in which to install Linux (page 65). You can also use the ubiquity partition editor "Install side-by-side..." on page 70.

- Remove a Windows partition
If you can delete a big enough Windows partition, you can install Linux in its place. To delete a Windows partition, you must have multiple partitions under Windows and be willing to lose the data in the partition you delete. In many cases, you preserve the data by moving it from the partition you will delete to another Windows partition. 

Once you are sure a partition contains no useful information, you can use a gparted (page 66) or palimpsest (page 69) to delete it. After deleting the partition, you can install Ubuntu Linux in the free space by removal of the partition.

## INSTALLING UBUNTU LINUX AS THE SECOND OPERATION SYSTEM

When enough free space on a Windows system is available (see the previous section), you can install Ubuntu Linux. The ubiquity Prepare disk screen, select Use the largest continuous free space (page 71). Alternatively, if you are installing Ubuntu on its hard disk, select Use the entire disk (page 71) and click the radio button next to the disk you want to install Ubuntu on. Click Forward. After the installation is complete, when you boot from the hard disk, you will be able to choose which operating system you want to run.

## ADVANCED INSTALLATION

This section explains how to install Ubuntu from each of the four disk menus: the DVD menu, the Desktop CD menu, the Alternate CD menu, and the Server CD menu. It also describes using the Ubuntu textual from the DVD.

Each menu screen includes a menu centered on the screen and a list of function keys and labels at the bottom. 3-3 on page 54 shows the DVD menu screen.

The Ubuntu DVD includes most of the selections from each of the CDs and includes all software packages supported by Ubuntu, not just those installed by default. If the system you are installing is not connected to the Internet, you can install software packages from the DVD but you will have no way to update the system.

The DVD menu

The Desktop CD can bring up a live session, install Ubuntu on a hard disk, and rescue a broken system.

The Desktop CD menu

The Server CD uses the textual overlay (page 85) to install a minimal system with a textual interface and no open ports. The installed system is appropriate for a server.

The Server CD menu

The Alternate CD uses the textual installer (page 85) to install a system that uses a graphical interface or one that uses a textual interface. It is not a live CD (i.e., it does not require as much RAM to install Ubuntu and presents more installation options than the graphical installer).

The Alternate CD menu

Ubuntu displays the language overlay (page 54) on top of these four menus. After you select a language from the overlay, you can work with the disk menu. The language you select from the language overlay is the default language. As you install Ubuntu, you can change the default language from the Welcome screen (page 58).

## THE DISK MENU SCREENS

Each of the four disk menus holds different selections. In addition, the f4 key displays different selections from each of these menus. This section discusses each of the menu selections and describes what happens when you press each the function keys from each of these menus. The final part of this section covers boot-line parameters.

## MENU SELECTIONS

The Minimal CD (page 32) does not display a menu, but rather displays a boot:prompt. Enter linux to start a textual installation from this disk or enter return to display more information.

| Name of CD/DVD | DVD | Desktop | Server |
| :--- | :--- | :--- | :--- |
| Try Ubuntu without installing | | | |
| Install Ubuntu | | | |
| Install Ubuntu in text mode | | | |
| Check disc for defects | | | |
| Test memory | | | |
| Boot from hard disk | | | |
| Rescue a broken system | | | |
| Install Ubuntu Server | | | |
| Install Ubuntu Enterprise Cloud | | | |

Table 3-1 shows the selections (based on text context).

The Desktop CD can bring up a live session, install Ubuntu on a hard disk, and rescue a broken system.

The Server CD uses the textual overlay (page 85) to install a minimal system with a textual interface and no open ports. The installed system is appropriate for a server.

The Alternate CD uses the textual installer (page 85) to install a system that uses a graphical interface or one that uses a textual interface. It is not a live CD (i.e., it does not require as much RAM to install Ubuntu and presents more installation options than the graphical installer).

The Minimal CD (page 32) does not display a menu, but rather displays a boot:prompt. Enter linux to start a textual installation from this disk or enter return to display more information.

The Ubuntu DVD includes most of the selections from each of the CDs and includes all software packages supported by Ubuntu, not just those installed by default. If the system you are installing is not connected to the Internet, you can install software packages from the DVD but you will have no way to update the system.

Ubuntu displays the language overlay (page 54) on top of these four menus. After you select a language from the overlay, you can work with the disk menu. The language you select from the language overlay is the default language. As you install Ubuntu, you can change the default language from the Welcome screen (page 58).

The DVD menu

The Desktop CD menu

The Server CD menu

The Alternate CD menu

The language overlay

Rescue a broken system—Provides tools to repair a system that may not boot or that has a problem with the mounted at /(root). see page 83.

Install Ubuntu Server—Installs a Ubuntu server using the textual installer. For more information refer to “The Ubuntu Installer” on page 85. During installation, the installer displays the selection screen, which asks you to install various servers, a DNS server (Chapter 24), a LAMP server (includes Apache [Chapter 26], MySQL [page 628], and PHP), and OpenSSH server (Chapter 18), a Samba server (Chapter 23), and others. Use the ARROW keys to move the highlight to the space between the brackets ([ ]) and the space bar to select a choice.

Install Ubuntu Enterprise Cloud—Brings up a private cloud. For more information see www.ubuntu.com/cloud/private.

The You can press ESC from any of these menus to display a prompt.

## THE FUNCTION KEYS

Along the bottom of each screen is a series of labeled key names. Pressing each function key displays information or a menu that may be helpful if you experience a problem while booting Ubuntu or in a live session. Some of the keys allow you to change parameters.

- F1 The F1 key displays the help window shown in Figure 3-21 (next page). Pressing a function key while this window is visible displays another help window. A function key when this window is not displayed has the effect described in the following paragraphs. Press ESC to close the help window.

- F2 Language The F2 key displays the language overlay (Figure 3-1, page 52). Use the Arrow keys to highlight the language you want the live session or the installer/installed system to use and press RETURN. Ubuntu gives you the opportunity to change this selection for the installed system as you install the system.
