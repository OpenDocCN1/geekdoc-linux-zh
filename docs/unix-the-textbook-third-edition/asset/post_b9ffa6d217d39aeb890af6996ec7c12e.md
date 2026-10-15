
are, even in larger capacities, having two automatically created copies of your files on this thumb drive is not prohibitive.

- d. Copy a number of important files into this new dataset from your systems hard drive using either the cp or rsync commands shown in Chapter 23.

- e. Instead of proceeding onto step 6 of the example, retain the zpool and dataset you have created on the thumb drive, and use it as a backup drive for your important files. You can periodically use rsync to keep the backup files synchronized to the important files on your hard drive. You may even decide that the important files you want to back up to the thumb drive are in a single directory or multiple directories. You can then use rsync to copy directories over to the thumb drive.

- f. To remove the USB thumb drive temporarily at any time, use the zfs unmount command. Then you can remove it from the computer. Remember to use the zfs mount command when you want to reinsert the USB thumb drive and archive or backup files to it.

## 10. Repeat Problem 24.9 on your Solaris system, but instead of using cp or rsync to move important files to the USB thumb drive from some arbitrary place(s), do the following:

- a. Create a new zpool on the hard drive which will be the source of your important files to be backed up.

- b. Put a dataset in that new pool and fill the dataset with important files you want to backup.

- c. Use the methods of Example 24.2 to create a ZFS snapshot of the new dataset created on your hard drive pool. Then, continuing the methods shown in Example 24.2, use zfs send and zfs receive to copy the snapshot from the hard drive to the USB thumb drive.

## 11. On a PC-BSD system, back up your home directory (or a selected subdirectory of your home directory) to a USB thumb drive using the commands zfs snapshot, zfs send, and zfs receive. The ZFS dataset for your home directory should be named something like tank/usr/home/your_username.

Be sure to insert and test the USB thumb drive you want to use for this problem, to find out if it is usable on your system. If it doesn't show up in /dev after insertion, it is not usable!

After testing the USB thumb drive for usability, make sure that automounting of removable media is turned off in System Settings. Prepare the USB thumb drive using the Disk Manager to destroy any partition table on it, and create a GPT partitioning table on it. Then use the gpart command to create one primary partition with a ZFS file system.

## 12. On a PC-BSD system, use an externally mounted USB hard drive to repeat the operations given in Example 24.6. Note any differences in using a hard disk on the USB bus and using a USB thumb drive.

## 13. An important use of the procedure that you will implement in this problem is to enable you to create a ZFS mirror of your system disk, so that you have redundancy of your system disk and data. This single, internally mounted hard disk vdev, which can also contain all of your user data files, may be inside of a laptop computer that can only have a single hard disk internally mounted. The mirror you will create in this problem is maintained over the USB bus. If the hard drive in the external (but openable) enclosure we designate here is a SATA drive, then that drive can also be used as a replacement for the internal, single SATA hard disk drive if that drive fails. The problem assumes that the external USB hard disk in its enclosure, and the internal hard disk in your computer, can be easily removed and reinstalled. They must also both be SATA drives, either spinning disk or SSD. This problem achieves the same objectives as those illustrated in Chapter 23 for Clonezilla Live.

On a PC-BSD system, use an externally mounted USB hard drive in an openable enclosure to repeat the operations given in Example 24.4. You must make sure that the capacity of this USB external drive is large enough to accommodate the creation of the mirror.

To test whether or not you have correctly solved this problem, shut down the system. Then remove the external USB hard drive from its enclosure, and replace the internally mounted hard drive in your computer with it. Your system should then boot from the new hard drive, but the mirror will show as being in a degraded state. Then replace original and external disks in the original configuration.

To repeat this procedure when your internal hard drive actually fails, follow the processes shown previously in the chapter for replacements of vdevs in a mirror.

## 14. Mansoor is working with Bob on a project. He needs to be able to read, write, create, and delete files related to the project, which are located in the Project directory of Bob’s home directory. Bob and Mansoor are ordinary users without administrative privileges. They wish to do this project without contacting the system administrator to request new groups, group membership changes, sudo changes, and so on.

When the project is over, Bob will remove the modify permissions on his home and the Project directory for user mansoor. By modify, we mean Mansoor can still look at the contents of the Project directory, but cannot make any changes to the files in it. He will do this himself, instead of contacting the system administrator.

On your own Solaris system, in conjunction with another user, use ACLs to accomplish the following (substituting valid usernames on your system for Bob and Mansoor):

- a. Create a project directory under Bob’s home directory named Project. On our system, the path to this new directory is /export/home/bob/Project.
- b. Set the ACL on Bob’s home directory so Mansoor has read, write, and execute privileges on it.
- c. Set the ACL on the Project directory so that Mansoor has rwxo privileges on it.
- d. Have Bob create some files in the Project directory.
- e. Have Mansoor make Bob’s home directory the current directory.
