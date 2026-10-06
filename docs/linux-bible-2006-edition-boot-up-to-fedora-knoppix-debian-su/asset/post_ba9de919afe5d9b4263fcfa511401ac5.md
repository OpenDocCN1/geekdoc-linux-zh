
# Chapter 17 ✦ Running Ubuntu Linux 449

**Erase entire disk and use LVM** — As the previous choice, your data is erased. However, when the Ubuntu installer creates new partitions, it creates partitions using Logical Volume Manager format. This allows you to easily increase existing partitions at a later time but make the partitions harder to use with some file system tools. For example, bootable Linux LiveCDs can't read LVM partitions.

**Manually edit partition table**— This lets you manually create your own hard partitions. This is the best choice if you want to keep existing partitions from being erased or if you have special needs, such as creating separate partitions to hold user (/home) or separate data (/var), or using a particular file system type for an area of your hard disk. Manual partitioning is considered to be a more advanced skill.

If you selected to manually edit the partition table, proceed to the next step. Otherwise, skip ahead to 11.

- 10. During the manual partitioning phase, you can choose to set up your LVM or RAID configurations (see Chapter 7 for details). However, if you simply want to deal with existing partitions, you can use up and down arrows to highlight an existing partition, and press Enter to select it. Here is the type of information you can set for each partition:

- **Use as** — Choose the file system type. Ext3 and ReiserFS are the most common file system types for custom desktop systems. JFS and XFS are used more often in high-accessibility systems. FAT16 and FAT32 can be used for file systems that you want to share with Windows systems. Swap space is selected as swap area system type.

- **Format the partition**—Select no to format the partition, keeping all data intact. Select yes to erase all data on the partition and format it.

- **Mount point**—You need to have a root partition (/) and a swap area. It is also common to have a /boot partition of about 100MB or 200MB. Other common mount points are also listed for you to select, or you can enter a mount point manually.

- **Label**— You can enter a label (which may or not be different than the mount point name).

- **Reserved blocks**— Indicates the percentage of file system blocks for the super user.

- **Typical usage**— You can change the way the file system is configured, based on the type of data it will contain. Standard usage is fine for desktop systems. However, a file system that will contain many small files (such as a new server) should choose the news option. That option will make many more inodes available for use on the file system (there must be a separate inode for every file and directory in a file system). For file systems that will contain very large files, you should select largefile (one inode per megabyte) or largefile4 (one inode per four megabytes).

- **Bootable flag** — Turn this on if the file system is capable of being booted (typically the `/boot` partition or / , if no boot partition exists).

- **Size** — Select if you want to resize the partition.

When you are done, select **Done setting up the partition** and press Enter. Repeat this process for all partitions. When you are done, select **Finish partitioning and write changes to disk** to continue. Review the partition (you still want to go back and fix any problems). When you are ready to begin rewriting your hard disk, select **Yes** and press Enter.

At this point, your hard disk (or disks) will be reformatted. The Ubuntu installer will begin installing the software you selected (desktop or server). This will take a while.

After the software is installed, you are asked to enter your time zone.

- 11. Select your time zone from the list provided (or to select a time zone that is not on the list) and press Enter. You are asked to add a username.

- 12. Select a full name (for example, John Smith) to assign to a username that you can use for non-administrative work on the system. You are asked to enter a username.

- 13. Select a username (for example, jsmith) to identify the user account. You are prompted to assign a password for that user.

- 14. Type in a password (twice) for the new user. The Ubuntu installer finishes the first stage of installation and ejects the CD.

- 15. Remove the installation CD and select Continue. Ubuntu reboots from the hard disk and continues the installation process. As individual packages require you to make choices about how they are installed, you will be prompted for further information. For example, you will be asked to configure video cards.

When installation is complete, Ubuntu reboots and displays the graphical login screen. If you have an Internet connection, the first thing you should do after logging in is to make sure you have the latest upgrades and security patches. To do that, open a Terminal window (select Applications 〈 System Tools ➜ Terminal) and type the following:

```bash
$ sudo apt-get update
Password:
```

After you enter your password, the apt-get utility will get all available updates for the software you have installed in Ubuntu.

# Chapter 17 ✦ Running Ubuntu Linux 451

If some reason, Ubuntu couldn't install all the software packages you wanted, you can open the Synaptic Package Manager Window (select System ↪ Synaptic Package Manager) or Add/Remove Applications window (select System ↪ Add/Remove Programs). Using that application, you can add the software you want individually. Software not available on the CD will be downloaded from the Internet.

# Starting with Ubuntu

On the surface, Ubuntu is not different from other Linux distributions. Underneath, the tools for managing your software are expected. Log in using your username and password. Figure 17-2 shows an example of the Ubuntu desktop.

![Ubuntu Desktop](img/a2d958d7e432b9b8aa70.png)

# Trying Out the Desktop

With the latest GNOME interface, menus are available from the top panel. By default, Ubuntu comes with many applications. The following list explains the categories you get:

- **Accessories** — From this menu, select some basic desktop utilities. Choose Archive Manager to launch File Roller, which provides a simple GUI for managing files. Text Editor starts the default text editor (so you don't have to use unintuitive vi). Browser starts Nautilus, which is the most common tool for navigating around. Other Accessories include a Calculator, a Character Map (for mapping special characters), and Dictionary (for checking word definitions).

- **Games** — Under the Games, you get a selection of GNOME games. Games are similar to those you would find on a Windows desktop (Mines, AisleSolitaire, and FreeCell Solitaire are examples). There are also Tetris-like games (Gnometris) and board games (Mahjongg). One of the more demanding open sources (such as Tux Racer) or networked games (such as the BZFlag tank battle game).

- **Graphics** — The Ubuntu desktop includes the GIMP open source graphics manipulation application. It also includes the Thumb and Eye of GNOME viewers. To import images from a scanner, Ubuntu includes the XImage scanning application. No document viewers are included here, such as Evince (which can be used to view PostScript and PDF files).

- **Internet** — Popular, standard open source Internet clients can be launched from this menu. Evolution (resource-intensive but full-featured Outlook-like email client) can be used for messaging and emailing. Firefox is the web browser and GAIM is for instant messaging. The Gnome Torrent client can be used to download files. GnomeMeeting lets you do video conferencing over a network. The Terminal Server Client provides a free remote terminal and viewer. XChat lets you use Internet Relay Chat (text-based) messaging.

- **Office** — A full set of OpenOffice office productivity applications are included with Ubuntu. Selections include OpenOffice Calc (spreadsheet), Draw (drawing and flowcharts), Impress (presentations), Math (formulas and equations), and Writer (word processing). OpenOffice.org Base lets you create and access a database.
