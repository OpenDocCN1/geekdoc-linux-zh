# Example 24.6: Creating a ZFS Pool on a USB Thumb Drive for PC-BSD

Be aware that destroying the zpool will then allow you to remove the USB thumb drive from the machine. If you want to use that thumb drive for another purpose, you may have to reformat it to FAT32 and erase the data on it.

Conclusion: You have created and destroyed a zpool on a USB thumb drive. If you did not destroy it, you can now have datasets placed on it, and directories and files. All of the ZFS commands in this chapter can be used to manage zpools and datasets on this drive. You can also use this drive as a backup for user data files. See Problems 24.9 and 24.10 at the end of the chapter.

Objectives: To create a zpool and a ZFS dataset in that pool on a thumb drive in PC-BSD.

Introduction:

The following example uses the most essential command in ZFS, the zpool command, with the subcommand create applied to a USB thumb drive on your PC-BSD system. The real power of ZFS on PC-BSD can be harnessed to common, readily available hardware vdevs that are available to place on the system by an ordinary user.

If the only thing you want to do is use a USB thumb drive to transfer files (such as text files, C program source code, LibreOffice documents, and so on) to and from the computer, you do not have to use the procedures of this example to accomplish that. Simply put the USB thumb drive in a USB port on the computer, and when the Mount Tray recognizes it, make the choice to mount it.

When finished transferring files, unmount it in the Mount Tray and remove it from the computer.

Many UNIX systems with a GUI interface, like Gnome or KDE, automatically mount the USB thumb drive on the file system, and make it available as a desktop icon. This is similar to what you would experience on non-UNIX systems. PC-BSD does not do this, for security and other administrative reasons. PC-BSD under KDE does make a system tray icon, known as the Mount Tray, available to allow you to semiautomatically mount things like USB thumb drives, and so on. It can be found in the lower-right corner of the screen, and if you right-click on it, you can make several pop-up menu choices affecting the Mount Tray.

From the KDE Kickoff Applications Launcher, you can make the System Settings menu choice. One of the System Settings icons is Removable Devices. When you click on this icon, you can turn automounting on or off, and also configure other settings for removable media. By default, automounting is off. This setting is independent of what the Mount Tray does. If you turn off automounting and quit the Mount Tray, mounting of removable media such as USB thumb drives or hard drives can be done manually.

If you make a mistake anywhere along the way, you can always start over by executing the cleanup step shown at the end of the example then begin again.