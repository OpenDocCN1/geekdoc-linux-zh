# Note

If you'd like to install a more flexible superuser command than su, try the sudo command. This program can be used to selectively extend superstatus to designated users for certain commands. For more information, navigate to http://www.courtesan.com/sudo.

# Creating a Boot Disk

One of the most important things to do during your Red Hat Linux install is to make a boot disk. You should always have a working copy on hand.

If you skipped creating a boot disk, don't worry! Because you're a Red Hat Linux user, you'll find Erik Troan's handy mkbootdisk command installed on your system. Use mkbootdisk to create an emergency boot disk you can use to boot Linux in case LILO or your boot manager gets wiped out.

First, log in as the root operator. Next, use the uname command with the -r, or release number, option on the command line of your console or X11 terminal window like this:

```
# uname -r
2.2.16-22
```

As you can see, the uname has returned 2.2.16-22 as the release number of the currently running Linux kernel. Next, use mkbootdisk with its -device option, followed by the device name of your floppy drive and the release number of your Linux kernel returned by the uname command:

```
# mkbootdisk --device /dev/fd0 2.2.16-22
```

Insert a blank floppy disk and press the Enter key. You then see this:

```
Insert a disk in /dev/fd0. Any information on the disk will be lost.
Press <Enter> to continue or ^C to abort:
```

Press Enter to make your boot disk. When the command finishes, remove the floppy, label it, and place it in a safe place.

Another method of safeguarding your system is to make a secondary backup set of two emergency disks that use a minimal filesystem. These disks can help get you started on the road to recovery if you run into problems. Some excellent guides, scripts, and software are available to help you create your own diskette set (see “For More Information,” at the end of this chapter). Generally, the approach is to create two disks, one containing a kernel and the other containing a compressed filesystem with a minimal directory of files, including file utilities.