might back up only your data files and then use your Windows CD-ROM and other application source disks to reinstall.

Even after making a complete backup, you still need an original Microsoft Windows CD-ROM or the equivalent set of floppy disks for reinstallation. That might not be true if you can back up over a network, or if you are running MS-DOS backup software. But if your backup software runs under Windows, you must first install the operating system from its original source, install your backup software, and then restore your files from your backups.

Warning

> Do not perform the following steps until you are sure that you can reinstall Microsoft Windows from an original CD-ROM or set of floppy disks, and that you can restore your backed-up application and data files.

After creating and verifying your backups, the next step is to create an MS-DOS boot disk. Insert a blank disk into drive A:, and from an MS-DOS prompt or a DOS window opened in Microsoft Windows, enter the following command (this erases all files on the disk):

```
format a: /s
```

The /s option copies system boot files to the disk. After formatting is done, copy to the disk the utility programs fdisk.exe, format.com, sys.com, and scandisk.exe that are probably located in C:\DOS or C:\Windows\Command. You might also want to save copies of your autoexec.bat and config.sys files, but be sure to rename them (or place them in a subdirectory on the disk) so that they aren't referenced during booting.

Next, boot to the MS-DOS disk. You are now going to allocate your hard-drive partitions and permanently erase all files on your hard drives. This is your last chance to back up your files. When you are ready to proceed (you should be seeing an A: prompt), enter fdisk to run the MS-DOS disk partitioning program. If you are asked whether to enable large disk support, answer no.

Select option 4 and write down all existing partition information in your installation log. Now, follow the next steps, which should be generally correct for most readers. However, depending on how many drives you have and their sizes, you might need to make specific changes to suit your system and needs. The following steps assume that you are dividing your system equally between Linux and Microsoft Windows:

+   1. Delete all logical drives one by one from the extended DOS partition, if there is one.
+   2. Delete the extended DOS partition.
+   3. Delete the primary DOS partition.
+   4. Create a new Primary DOS Partition using 25% to 50% of the hard drive. This must be the first partition. You will install Microsoft Windows to this partition.
+   5. Set the active partition to the Primary DOS Partition that you just created.
+   6. Optionally create a new extended DOS partition using 25% of the hard drive, or however much space you want. I like to do this to create a separate partition for my data files.