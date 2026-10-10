# **KDE 1.0 drives**

CD-ROM drives by using /auto/... as the path to the file. Do not use /mnt/floppy as the route to the floppy drive or use the mount and umount commands when the /auto/floppy route is in use. Similarly, if you are using /auto/cdrom to reach the CD-ROM drive do not use the /mnt/cdrom route, or try to mount or umount the drive.

If you placed KDE 1.0 things are less straightforward. The disc icons have to be used in the KDE 1.1 if you so wish, which is not difficult. You can also do things this way in KDE 1.1 if you so wish, which would seem to be pointless. Login and then run the KDE program, Right-click on a vacant area of the desktop and select New and select Device or File System Device in the dialog that appears (Figure 4.10). You must enter the filename for the icon, and you should replace "Device" in the default name with something appropriate such as "Floppy" or "CDROM". Leave the "Kernel" part of the filename unaltered. After you have exited this window a new icon will appear on the desktop, but so far it is not configured so that it will be useful.

![](bbox=[0.23, 0.5, 0.36, 0.66])

Fig. 4.10  The edit box used to name the KDE link file

It can be configured by right-click on it and select Properties from the pop-up menu. In the window that appears (Figure 4.11) select the Device tab, and then in the Device box type "/dev/d0" for a floppy disc icon or "/dev/cdrom" for a CD-ROM icon. Leave the other boxes untouched. The Properties tab, the icons for the devices must be selected. It is a case of icons after the icons for the other types of devices. It is a case of icons that appear a bit different depending on which tab you are in. Next, on the Floppy Disc tab select the device mounted button near the bottom of the window. From the six small green buttons choose the one that looks like a floppy disc with a small green square beside it, or its CD-ROM counterpart, as appropriate. Then, right-click on OK and then repeat the process using the green button, Left-click on Cancel, and you will have just named the icon. If you click on OK, the icon should look like Figure 4.12. Left-click on the icon should change from the question mark to the unmounted disc version.

It is important to realise that once the icons are in place they can not be used in place the same careful manner as use either the CD-ROM drive first install a disc and then right-click on the appropriate icon. This produces a small pop-up menu from which the Mount option should be selected. The drive s icon should change from the plain version "drive". You can also right-click on the green mount icon in the "Mount" menu, and on left-click on "Unmount", or on either icon to view the contents using KFM. Files can then be copied, moved, etc., in the usual way.

When you have finished using the disc it should not simply be removed from the drive. In the case of the CD-ROM drive the object will probably be locked by the system, and it will not be possible to eject the disc by simply pulling it out. Before a disc is removed it should be unmounted. To do this right-click on the drive s icon and select Unmount from the pop-up menu. The icon should then change back to the plain version, and it is then safe to remove the disc.

This is obviously far less convenient than using the floppy and CD-ROM drives in KDE 1.1. Also, set-up of the system, setting up your CD-ROM on the system, setting up drives for root" users than to access. It will almost be easy. It might not be necessary to edit the/etc/fstab file in order to make the/etc/fstab file in order to make the drive icons available to non-privileged

![](bbox=[0.74, 0.06, 0.91, 0.21])

Fig. 4.11 Setting the mount point

![](bbox=[0.74, 0.25, 0.91, 0.4])

Fig. 4.12 Choosing the drive icons