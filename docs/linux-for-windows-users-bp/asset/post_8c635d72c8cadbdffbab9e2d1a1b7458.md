
## Fig.4.6 The form used to enter or edit account details

![Fig.4.6](img/147f057d2f063d8c60ee616870537a94_70_0.png)

Open Administration System, which enables all manner of system settings to be viewed and controlled. To bring up the window that governs user accounts, activate the “K” menu and then select COAS, System and Accounts. This should bring up a window of type 4.4. This initial screen enables some basic account details to be read, and the Actions menu permits accounts to be edited or created. If the Create option is selected, the login name for the new account is first entered into a dialogue box (Figure 4.5) and then other details such as the full name of the user and the password are added to the form that appears (Figure 4.6). Where possible it is clearly easier to manage accounts using this sort of graphical front-end than it is via the command line.

## KDE and discs

The way in which KDE handles discs is not quite the same in versions 1.0 and 1.1. In fact KDE 1.1 handles floppy discs and the CD-ROM in a much more convenient manner, and it is worth upgrading from 1.0 to 1.1 for this factor alone. As pointed out in Chapter One, running KDE 1.1 for the first time can be greeted by a Windows-style Wizard (Figure 4.7) and taken through a series of screens that enable the program to be set up to suit individual preferences. One of these screens enables the user to select whether or not to have icons on the desktop for two floppy disc drives and the CD-ROM drive (Figure 4.8). I would strongly recommend having the icons as they make it very easy to access the floppy drives and the CD-ROM drive. (Of course, if your computer does not have “floppy 2” (the equivalent of disc B in MSDOS or Windows) you do not need the icon for this. If you did not have these icons added when KDE was first run, they can be added at a later date by running the KDE Configuration Wizard again. Operate the “K” button in the Panel, then select Utilities and KDE Configuration Wizard from the menu system.)

## Fig.4.4 The COAS user accounts editing window

![Fig.4.4](img/147f057d2f063d8c60ee616870537a94_70_1.png)

All three groups would then be available to a file owned by “Fred” (Figure 4.3). Of course, if you log in as “root”, all things are possible, and all file available groups will be available as “root” in the Permissions window. Any file can then be assigned to any group.

Depending on the version and distribution of Linux you are using you may be able to accomplish tasks as an administrator via a graphical user interface. Caldera Open Linux 2.2 has the COAS (Caldera Open Administration System), which enables all manner of system settings to be viewed and controlled.

## Fig.4.5 The account name edit box

![Fig.4.5](img/147f057d2f063d8c60ee616870537a94_70_2.png)

## Fig. 4.7 This wizard appears the first time KDE is run

![Fig. 4.7](img/147f057d2f063d8c60ee616870537a94_71_0.png)

If you do select the disc icons, the appropriate icons should be added to the desktop beneath KDE desktop, and that this set-up process has to be repeated for each user. In order to access a standard CD-ROM you can simply place it in the drive and then click on the CD-ROM icon. This will launch a KFM window that displays the contents of what is the root directory of the CD-ROM in M$DOS/Windows terminology. In the Linux file system the CD-ROM is at /auto/cdrom or /cdrom as you might expect. This is not purely of academic importance, as this method offers significant advantages. There is no need to mount and unmount CD-ROMs. If you have finished with one CD-ROM and wish to use another, simply remove the first CD-ROM and replace it with the second one. If you then left-click on the reload button the KFM window will change to show the contents of the new CD-ROM.

Things work in much the same way, with floppy discs, and these are also freely accessible to the file system and user. You can also change the system as you would on a Windows system. When using applications you can save directly to the floppy disc by using /auto/floppy1/filename. We are assuming here that only one floppy drive is present in the system. The appropriate “floppy” and “floppy1” must be used in place of just plain “floppy”. You can also load from the floppy or

## Fig. 4.8 The easy way to add icons for discs in KDE 1.1

![Fig. 4.8](img/147f057d2f063d8c60ee616870537a94_71_1.png)

## Fig. 4.9 The added disc icons

![Fig. 4.9](img/147f057d2f063d8c60ee616870537a94_71_2.png)

## **KDE 1.0 drives**

CD-ROM drives by using /auto/... as the path to the file. Do not use /mnt/floppy as the route to the floppy drive or use the mount and umount commands when the /auto/floppy route is in use. Similarly, if you are using /auto/cdrom to reach the CD-ROM drive do not use the /mnt/cdrom route, or try to mount or umount the drive.

If you used KDE 1.0 things are less straightforward. The disc icons have to be used in the KDE 1.1 if you so wish, which is not difficult. You can also do things this way in KDE 1.1 if you so wish, which would seem to be pointless. Login and then run the KDE program, Right-click on a vacant area of the desktop and select New and select Device or File System Device in the dialog that appears (Figure 4.10). You must enter the filename for the icon, and you should replace "Device" in the default name with something appropriate such as "Floppy" or "CDROM". Leave the "Kernel" part of the filename unaltered. After you have exited this window a new icon will appear on the desktop, but so far it is not configured so that it will be useful.

## Fig. 4.10 The edit box used to name the KDE link file

![Fig. 4.10](img/147f057d2f063d8c60ee616870537a94_72_0.png)

It can be configured by right-click on it and select Properties from the pop-up menu. In the window that appears (Figure 4.11) select the Device tab, and then in the Device box type "/dev/d0" for a floppy disc icon or "/dev/cdrom" for a CD-ROM icon. Leave the other boxes untouched. On the Properties tab, the icons for the devices must be selected. It is a case of selecting icons that appear a bit different depending on which tab you are in. Next, on the Floppy Disc tab select the device mounted button near the bottom of the window. From the six small green buttons choose the one that looks like a floppy disc with a small green square beside it, or its CD-ROM counterpart, as appropriate. Then, left-click on OK and then repeat the process using the green button. Left-click on Cancel, and you will have just named the icon. If you click on OK, the icon should look like Figure 4.12. Left-click on the icon should change from the question mark to the unmounted disc version.

It is important to realise that once the icons are in place they cannot be used in the same careful manner as in KDE 1.1; you must use the CD-ROM drive first, install a disc and then right-click on the appropriate icon. This produces a small pop-up menu from which the Mount option should be selected. The drive’s icon should change from the plain version to the mounted version. You can also right-click on the green mount icon in the "Mount" menu, and on left-click on "Unmount", or on either icon to view the contents using KFM. Files can then be copied, moved, etc., in the usual way.

When you have finished using the disc it should not simply be removed from the drive. In the case of the CD-ROM drive the object will probably be locked by the system, and it will not be possible to eject the disc by simply pulling it out. Before a disc is removed it should be unmounted. To do this right-click on the drive’s icon and select Unmount from the pop-up menu. The icon should then change back to the plain version, and it is then safe to remove the disc.

This is obviously far less convenient than using the floppy and CD-ROM drives in KDE 1.1. Also, set-up of the system, setting up your CD-ROM on the system, setting up drives for "root" users than to access. It will almost be easy. It might not be necessary to edit the /etc/fstab file in order to make the drive icons available to non-privileged users.

## Fig. 4.11 Setting the mount point

![Fig. 4.11](img/147f057d2f063d8c60ee616870537a94_72_1.png)

## Fig. 4.12 Choosing the drive icons

![Fig. 4.12](img/147f057d2f063d8c60ee616870537a94_72_2.png)
