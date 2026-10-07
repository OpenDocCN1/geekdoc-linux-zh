To set up partitions for Linux, remove any existing partitions first (unless you want to keep them as they are). If you intend to use DOS on the same system as Linux, DOS should be the first partition on the disk so it can boot. (There are a few ways to get by this using LILO, but it is still a good rule to leave DOS as the first partition.) If you are keeping an existing DOS partition, leave at the first partition as DOS.

You should create a DOS boot disk, which can reformat and transfer the DOS kernel to the hard drive, regardless of whether you are leaving an existing DOS partition or creating a new one. To create the boot disk, use this DOS command (assuming A: is the drive the disk is in):

```
format a:/s
```

The /s option transfers the operating system kernel. Next, copy the utilities FDISK, FORMAT, SYS, and CHKDSK to the boot floppy. You should also copy an editor, such as EDIT, as well as your existing CONFIG.SYS and AUTOEXEC.BAT files (although you could rename them). This disk lets you format any new DOS partitions. Alternatively, if you are starting from scratch with a new DOS partition, you can simply reload DOS from the original disks when you're ready to format the DOS partition.

If you are removing an existing DOS partition and re-creating a smaller one (as you would if your entire disk were DOS before Linux came into your life), follow these steps (after making a backup of your DOS data):

+   1.  Remove the existing DOS partition.
2.  Create a new primary DOS partition as the first partition.
3.  Make the DOS partition active.
4.  Reboot the system from your boot floppy (or DOS disks).
5.  Format the DOS partition and transfer the DOS kernel (COMMAND.COM).
6.  Restore your backup files to the DOS partition (this can be done at any time).

Next, set up the Linux swap space partition by creating a partition of the proper size. You can do this step either from DOS or when you have booted Linux from the boot and root floppies. For the sake of this chapter, it is assumed that you are setting up the partitions from DOS, although the process is the same either way.

Most versions of fdisk allow you to enter the size of the partition in megabytes, with the utility calculating the sector numbers that apply to it. Set the size of the Linux swap space to whatever size you decided, to a maximum of 16MB. Don't make the partition active or format it! You can set up the swap space partition in an extended disk partition, but a primary partition is a better choice if your disk can support it.