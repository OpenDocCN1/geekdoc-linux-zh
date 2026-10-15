9. When ready, you can quit the PC-BSD Disk Manager by clicking on the destroy button in the upper right-hand corner of the window, and you can also exit from the root terminal you launched in step 2.

# Example 23.5: Adding an External USB Hard Drive and Partitioning It in PC-BSD

A common postinstallation addition to a PC-BSD system is of an external USB hard drive that needs to be formatted and partitioned before it can be mounted and used on the system.

The following instructions assume you already have an internally mounted hard disk on your system to begin with; on our system it is listed as ada0. You should deploy the methods shown in Section 23.4.2 to find out the logical name of the new disk you want to add. USB drives usually are designated as daXpY, where X is a number starting at 0, and Y is a number starting at 1.

The instructions work for adding external USB hard disks, SATA or IDE, usually mounted in a powered enclosure. They also show how to detach that drive from the system. After the first step, they also assume that it is partitioned and formatted in such a way as to be incompatible with the PC-BSD system. If the disk you are adding does not appear in the /dev listing as a new disk you cannot easily use it on your system without obtaining the device drivers for it.

Also, from the KDE4 Kickoff Applications Launcher, you can make the System Settings menu choice to affect the automounting process of USB removable media. One of the System Settings icons is Removable Devices. When you click on this icon, you can turn automounting on or off, and also configure other settings for removable media. By default, automounting is off. The Mount Tray, a KDE4 desktop icon, is shown in the Panel as item F in Table 22.4, and illustrated in Chapter 22, Figure 22.12, "KDE4 Panel components." It allows for easy, GUI-based management of removable media that you can add to or remove from the system.

+   1. Power on the external hard drive enclosure, and connect the USB cable from the enclosure to a USB port on the computer. At this point you could determine the logical device name of the newly added external USB drive using the methods shown in Section 23.5.2. But we show how to do this in the following steps using Disk Manager.