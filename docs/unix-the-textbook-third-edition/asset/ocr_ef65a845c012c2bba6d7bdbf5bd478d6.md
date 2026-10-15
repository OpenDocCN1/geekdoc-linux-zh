are, even in larger capacities, having two automatically created copies of your files on this thumb drive is not prohibitive.

+   d. Copy a number of important files into this new dataset from your systems hard drive using either the cp or rsync commands shown in Chapter 23.

+   e. Instead of proceeding onto step 6 of the example, retain the zpool and dataset you have created on the thumb drive, and use it as a backup drive for your important files. You can periodically use rsync to keep the backup files synchronized to the important files on your hard drive. You may even decide that the important files you want to back up to the thumb drive are in a single directory or multiple directories. You can then use rsync to copy directories over to the thumb drive.

+   f. To remove the USB thumb drive temporarily at any time, use the zfs unmount command. Then you can remove it from the computer. Remember to use the zfs mount command when you want to reinsert the USB thumb drive and archive or backup files to it.

# 10. Repeat Problem 24.9 on your Solaris system, but instead of using cp or rsync to move important files to the USB thumb drive from some arbitrary place(s), do the following:

+   a. Create a new zpool on the hard drive which will be the source of your important files to be backed up.

+   b. Put a dataset in that new pool and fill the dataset with important files you want to backup.

+   c. Use the methods of Example 24.2 to create a ZFS snapshot of the new dataset created on your hard drive pool. Then, continuing the methods shown in Example 24.2, use zfs send and zfs receive to copy the snapshot from the hard drive to the USB thumb drive.

# 11. On a PC-BSD system, back up your home directory (or a selected subdirectory of your home directory) to a USB thumb drive using the commands zfs snapshot, zfs send, and zfs receive. The ZFS dataset for your home directory should be named something like tank/usr/home/your_username.

Be sure to insert and test the USB thumb drive you want to use for this problem, to find out if it is usable on your system. If it doesn't show up in /dev after insertion, it is not usable!

After testing the USB thumb drive for usability, make sure that automounting of removable media is turned off in System Settings. Prepare the USB thumb drive using the Disk Manager to destroy any partition table on it, and create a GPT partitioning table on it. Then use the gpart command to create one primary partition with a ZFS file system.

# 12. On a PC-BSD system, use an externally mounted USB hard drive to repeat the operations given in Example 24.6. Note any differences in using a hard disk on the USB bus and using a USB thumb drive.