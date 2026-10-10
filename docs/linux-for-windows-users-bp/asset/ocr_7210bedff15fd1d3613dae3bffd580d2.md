order to work your way through the material in this chapter. KDE 1.1 is
preferable, and if possible installations equipped with version 1.0 should
be upgraded. Most of the material provided here is relevant to both
versions, and where necessary any large differences between the two
versions are pointed out.

With some Linux distributions KDE is run automatically once Linux has
booted-up, to do this it is just a matter of logging in as usual and then using
this command:

```
kde
```

The program may be called KDE, but in order to run it you must type
'kde' rather than 'KDE'. The two versions are very similar in operation,
but there are some important differences. One of these becomes
apparent when you first run KDE. With version 1.0 you go straight into
your desktop, but with version 1.1 it is a Window style
program called "Kicker", and in a sense you are in a setup mode for the
desktop until you are completely set up for immediate use.
As a point of interest the KDE login screen on BEOS or MacOS on the
Macintosh is very similar. You have the option of starting KDE as
root, but this should be avoided. As the default user is normally set to
the standard KDE window manager. It would suggest that you settle
for root as a desktop at any time, but initially I would suggest that you settle
for standard KDE window locks.

Another difference is that version 1.1 will optionally add icons for the
floppy disc or discs to the desktop, plus an icon for the CD-ROM. I
would suggest that you let KDE add icons for these as the icons make
it much easier to use the floppy drive or drives and the CD-ROM
drives, as you can simply just drag an item to the appropriate icon to
do the operation you want, for example to add icons for these
things at an early stage. This is covered in the section of this chapter
that deals with the use of disc drives.

# The desktop

Once into KDE the screen should look something like Figure 3.1. If you
have used any form of Windowsing environment the KDE desktop should
look slughty familiar, but there are some aspects that will not.

# Trash

The Trash icon is equivalent to the Trashcan in some operating systems,
similar to the Recycle Bin in Windows. The icons representing files can be
dragged to the Trash icon and dropped there to delete them. This is the
KDE equivalent of the command line `rm` (remove) command, but like
the Windows Recycle Bin files are not destroyed when they are dropped
into the trash icon. They are moved from their original location into a

![](bbox=[0.45, 0.05, 0.55, 0.42])

directory for deleted files. They remain in that directory until Trash is
emptied, and can be recovered if they have not been dumped.

This is very similar to the Windows recycle bin, but one important
difference is that files deleted from floppy discs are stored in a Trash until
it is emptied. With Windows a file on a floppy disc that is placed into the
Recycle Bin is actually deleted onto the disc and is not copied (possibly
with the 'add to last minute possible to recover the file, except (possibly)
to copy the file to a new account where it can be copied back to the original
disc, or anywhere else.

The icons on the desktop simply provide immediate access to a certain
point in the file system. If you login as 'root', the trash folder will be
/home/Desktop/Trash'. If you login as (say) 'Fred', the trash folder will be
/Fred/Desktop/Trash'. Deleted files are stored in this folder until
the trash is emptied, and then they can be treated just like any
other files in that folder. In the case of a hard disc file, take any
opportunity to delete the file. The files in Trash are stored on the hard disc, and
are not deleted immediately. In fact deleting files on
the hard disc can sometimes take a lot of time. The files in Trash are stored on the
hard disc and reduce the amount of free storage space.