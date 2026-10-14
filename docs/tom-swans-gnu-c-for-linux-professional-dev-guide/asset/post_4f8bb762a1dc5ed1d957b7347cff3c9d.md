
Because this makes the zip disk appear to be an msdos hard drive, you can use Linux commands to access files and directories just as you can with a mounted hard drive partition such as /mnt/msdos. You don’t have to use the mcopy and mdir commands, which are intended for use only with MS-DOS floppy disks.

## CREATING LINUX ZIP DISKS

Although you can use MS-DOS-formatted Iomega zip disks with Linux commands, better performance is possible by installing a Linux file system. This also makes zip disks ideal for backups. For example, to back up the directory and all its files for this book, I simply enter these commands:

```
$ mount /mnt/zip
$ cp -a gpl /mnt/zip
$ umount /mnt/zip
```

The gpl—GNU Programming for Linux—in this command is the directory where I store this book’s files. The -a option, for “archive,” is just a simple way to copy many files and directories with one command. To use a zip drive this way on your system, you need to install a file system on the disk. You also might want to modify /etc/fstab so that you can mount and unmount zip disks without having to become the super user. However, you must be root to perform these steps, so enter this command first:

```
$ su
Password:
```

> Note
> Do not mount a zip disk before formatting. If you are not sure whether it’s mounted, unmount the disk by typing umount /mnt/zip.

Next, follow these steps to install a Linux file system on a zip disk. This removes all existing files from the disk, so be sure you want to do that before continuing. I assume here that the Iomega drive device name is /dev/hdd, which might be different for you. Because zip disks are configured as hard drives, they have partition tables that you can examine using the Linux fdisk utility. With a zip disk inserted but not mounted, enter this command:

```
$ /sbin/fdisk /dev/hdd
```

> Warning
> Be extremely careful when running the fdisk utility. Some of its commands permanently erase files. Remember also that you are the super user, and your powers include read and write permission for all files. Finally, be aware that the fdisk utility might understand different commands than described here, or it might have an entirely different display depending on the version of Linux you are running. Consider the following instructions as suggested guidelines only and proceed with caution.

## GETTING ONLINE INFORMATION

Use the Linux info utility to view online information about operating system commands, GNU C++, and dozens of other topics. The info utility is intended to replace the age-old UNIX man program—not a sexist reference, but an abbreviation for "manual." Although man is available in Linux, the info program generally gives more up-to-date information.

To use info, type its name at a console prompt optionally followed by the name of the item you want to know more about. For example, enter the following command for information about the Emacs programmer's editor:

```
$ info emacs
```

When you are finished viewing information, type q to quit info and return to a console prompt. Some info topics seem to be case sensitive, so if an info command doesn't work, check the exact spelling of the item you are trying to find. For a tutorial on using the info utility, type info info. For help using man, type man man or info man.

Throughout this book, I suggest various info pages you might like to view for more information about a subject. However, don't wait for me to suggest info to answer any questions you might have while reading this book. In time, you'll find info to be one of the most useful information utilities at your disposal.

## SUMMARY

It is my sincere wish that you are reading this summary after happily and successfully installing Linux on your computer. It's difficult in one small chapter to provide a complete guide to installing and configuring an operating system as large and as capable as Linux, but this chapter should have given you a springboard for getting started as well as providing tips for formatting and using hard drives, floppy disks, and Iomega zip disks. Steps in this chapter suggested ways to create standalone Linux systems, and dual-boot systems for Linux and Microsoft Windows. The next chapter explains how to install the GNU C++ compiler, if necessary, along with this book's listing files.
