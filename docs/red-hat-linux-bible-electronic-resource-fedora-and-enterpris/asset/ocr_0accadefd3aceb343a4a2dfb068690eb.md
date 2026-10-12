FIPS works by changing the values in the partition table and boot sector. Space is gained by changing the partition table that is used to create a new primary DOS partition. After that, the new DOS partition can be converted to Linux partitions.

> **CAUTION:** Warnings that come with FIPS documentation have mostly to do with older, nonstandard hard disks. I recommend reading the warnings that come with this documentation. You can find them on the Red Hat Linux installation CD #1 in the dosutils/fipsdocs directory. Especially read fips.doc.

Split your DOS (Windows) disk into separate DOS and Linux partitions as follows:

+   1.  **Check your Windows/DOS partition.**
+       In a DOS window, run chkdsk to check for disk errors. The output shows how your disk space is used, as well as errors found and corrected. Next, run scandisk in Windows 9x/2000. Scandisk deals with lost file fragments, invalid filenames, and cross-linked files. It also scans for disk surface errors. The point is to correct hard disk errors encountered.

+   2.  **Create a bootable FIPS floppy.**
+       You need to create a bootable floppy disk. Insert a blank, 3.5-inch floppy disk in drive A. Then, from DOS (or a DOS window), type the following to create a boot floppy:
+   
+   ```text
+   format a:/s
+   ```
+   
+       After creating the boot floppy, copy the following files from the first Red Hat Linux installation CD (CD #1) to this bootable floppy: restorebb.exe, fips.exe, and errors.txt. (These files are located in the dosutils/fips20 directory.) To make sure that the bootable floppy is working properly, insert the floppy disk into a PC that has a DOS (Windows 9x/2000) partition and reboot the computer. Now make sure that you can access the partition by typing dir C:\ at the prompt.

+   3.  **Defragment your hard disk.**
+       Reboot your PC so that Windows 9x/2000 starts up. To defragment your disk, so that all of your used space is put in order on the disk, open My Computer, right-click your hard disk icon (C:), select Properties, click Tools, and select Defragment Now.
+   
+       Defragmenting your disk can be a fairly long process. The result of defragmentation is that all the data on your disk are contiguous, creating a lot of contiguous free space at the end of the partition. There are cases where you will have to do the following special tasks to make this true:

+   *   If the Windows swap file is not moved during defragmentation, you must remove it. Then, after you defragment your disk again and run FIPS, you will need to restore the swap file. To remove the swap file, open the Control Panel, open the System icon, and then click the Performance tab and select Virtual Memory. To disable the swap file, click Disable Virtual Memory.
+   *   If your DOS partition has hidden files that are on the space you are trying to free up, you need to find them. In some cases, you won't be able to delete them. In other cases,