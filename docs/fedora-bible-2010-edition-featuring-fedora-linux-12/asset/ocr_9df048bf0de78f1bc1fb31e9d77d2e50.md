```
BURN-Free was never needed.
     wodm: fifo had 5331 puts and 5331 gets.
     wodm: fifo was 0 times empty and 5262 times full, min fill was 96%.
```

> NOTE: This output mentions wodm as that is the command actually run when you type in cdrecord. These commands are interchangeable. I used cdrecord on the command line for the examples because most users are more familiar with cdrecord.

After cdrecord finishes writing the CD and your shell prompt returns, delete the file system image file /var/tmp/marv.iso. Label the CD appropriately and store it in a safe place.

If you need any files that were copied to the CD, just return the CD to the CD drive. If it doesn't automatically open a window displaying the contents of the CD, type mount /media/cdrecorder. Open /media/cdrecorder in a folder window and copy the files you want.

Note that the mount point name for the CD drive may be something other than /media/cdrecorder. The way that the udev facility works in the latest version of Fedora is to use generic names such as cdrecorder, disk, or cdrom for CDs or DVDs that include no volume ID. However, if a volume ID was added to the CD header when the CD was created, that name will be used as the mount point. For example, a game CD with a volume ID of GAMEDISK would be mounted as /media/GAMEDISK.

> CROSS-REFERENCE: See Chapter 7 for more information on cdrecord. You can also learn more about installing and troubleshooting writable CD drives from the CD-Writing-HOWTO. If you are using a desktop Fedora system, you might want to use a graphical CD writer instead. Chapter 7 also describes the Brasero graphical tool for copying and burning CDs and DVDs.

# Writable DVD drives

In previous versions of Fedora, the dvdrecord command was used to write DVDs. Now, cdrecord can be used to write both CDs and DVDs. Using a writable DVD drive and the cdrecord command, you can back up your data to DVD-R, DVD-RW, DVD+R, and DVD+RW disks.

> NOTE: DVD-R is a write-once DVD format with a capacity of about 4.7GB. Discs in the DVD-RW format can be written and rewritten many times. DVD+RW is a read-write format that provides for faster writing of data, and DVD+R is a similar write-once format. Typically, a DVD-burning drive will support the plus (DVD+RW, DVD+R) or the minus (DVD-RW, DVD-R) formats. Some drives support both. It is important you purchase discs compatible with your hardware.

The first trick with recording to DVDs in Linux is to make sure that you have a drive that supports DVD writing. You can check by removing any disks in the CD/DVD drive and typing the following: