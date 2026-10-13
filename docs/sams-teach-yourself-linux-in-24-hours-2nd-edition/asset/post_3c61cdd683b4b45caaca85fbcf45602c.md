
## Using the cpio Command to Backup and Restore

The cpio, or copy in and out, command can be used in much the same way as the tar command, but with several differences, especially with archive creation or extraction command-line options. For example, to create a cpio archive, you must use the -o, or create, option. The cpio command also requires a list of filenames, with paths, to build an archive. To do this, use the find command, which handily creates the required names for you.

For example, if you have a directory called x11 that contains a number of files you want to archive, you can combine the output of the find command with the cpio command to build the archive, as follows:

```
# find x11 | cpio -ov >x11.cpio
cpio: x11: truncating inode number
x11
x11/xfree86faq.txt
x11/xappsfaq.txt
x11/x11faq.txt
x11/disaster.txt
x11/XHints1.txt
1082 blocks
```

This command line shows that the cpio command has been fed the names of the files inside the x11 directory, creating an archive with the -o option and showing you the files being added with the -v option. The name of the archive is x11.cpio, and it is created using the greater than, or >, redirection operator.

```
# cpio -i < x11.cpio
1082 blocks
```

This command line shows that to extract a cpio archive, you can use the less than, or <, redirection operator in conjunction with the cpio -i extract option. The cpio program recreates the directory and finishes by printing the number of 512-character blocks that were written to your hard drive.

You also can use the combination of the find command and cpio to create archives of any directory or even different files on your system. To back up all files in your directory that belong to you and have been created or modified during the current day, you can use the find command's -user and -mtime command-line options:

```
# find /home/bball -user bball -mtime -1 -print | cpio -o >today.cpio
```

This command line creates a cpio archive called today.cpio that contains all files you've modified in the last 24 hours. You're only limited by your imagination in how to devise your backups and how to back up your system. For more information on the cpio command, read its manual page. For more information about the find command, see Hour 5, or read the find manual page.

## Using the taper Script for Tape Drive Backups and Restores

The taper program, by Yusuf Nagree, is a backup and restore program used to create compressed or uncompressed archives of selected files or directories. This program provides a nice interface to create and maintain tape archives. You also can use other types of media to do your backups.

Using the taper command is easy. Specify the type of media to use with the -T media option. According to the latest documentation, the taper command supports the following options:

- ftape—floppy drive tape driver that is included with your system and is used for tape drives that attach to the floppy interface
- zftape—more recent floppy drive tape driver that handles additional tape formats
- scsi—driver for tape drives using a scsi interface
- ide—driver to support ide tape drives
- removeable—driver to support floppies, or removeable hard drives

If you don't have a tape drive but would like to try the taper program to test a backup of a directory to floppy diskettes, use the -T command-line option with the removable option:

```
# taper -T removeable
```

This starts the taper program, as shown in Figure 23.8. taper uses the default removable device, /dev/fd0, which is the floppy. To change the type of device to use a Zip disk, scroll down to the Change Preferences item, and press Enter. In the following dialog box, press Enter at the Tape Drive Preferences item.

In the Tape Drive Preferences dialog box, as shown in Figure 23.9, change both instances of /dev/fd0 to /dev/sda4, which is the default Zip disk device. Press Esc, and return to the main menu. In the main menu, press Enter at the Backup Module item.

### FIGURE 23.8

The taper script provides a graphic interface for archives or backup operations of directories and files.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_540_0.png)

### FIGURE 23.9

You can use different backup devices, such as /dev/sda4, for a Zip disk during your taper backup operations.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_540_1.png)

In the taper selection dialog box, as shown in Figure 23.10, you're asked to select files or directories before you start the backup. Scroll through the list of directories and files, and select items by pressing the I key. To get help, press the H or ? keys. When you finish, press the F key to start the backup operation.

The taper program has many different features. Its documentation is under the /usr/doc/taper directory in the file FAQ.txt.

### Figure 23.10

Scroll through the taper selection dialog box, selecting files or directories to back up with the I key.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_541_0.png)

## Summary

This hour introduced you to different programs and ways to back up your OpenLinux system. Performing periodic backups is an important role for a system administrator, and perfecting the practice of preserving your system and important files enhances your computing experience.

## Q&A

Q I don't want to use floppies to back up my system. I don't have a removeable hard drive. I also don't have a tape drive. What's the safest approach I can take to back up important files?

A You can at least back up your /etc directory. This directory probably contains fewer than 2.5 megabytes of files, which can be backed up to two floppy disks. Another method you can use is to back up important files to another partition (such as a mounted msdos or vfat partition). If you have the hard drive space, you can also create a small spare Linux ext2 partition to hold periodic backups of your system's configuration files. If something happens to your root partition, you can then restore from this spare partition.

Q Help! My system has crashed! I didn't back up my files! What can I do?

A First, don't panic! You did back up your important files, right? Do you have an emergency boot disk on hand? It might be possible to recover some files by booting with the emergency boot disk and then attempting to mount your OpenLinux partitions with the boot disk's mount command. If your Linux partitions still exist, it might also be possible to dump the contents of a partition to a compressed file on another volume and then extract pertinent files by hand (although this is tedious and not guaranteed). Always have a boot disk with recovery utilities on hand!

Q What's the best backup medium to use?

A There are many different types of removeable media on the market today. In the last 10 years, the price and cost per megabyte (a possible yardstick) of removeable optical drives has come down quite a bit. You have to decide on a balance of cost, speed, and reliability. You already have a wonderful backup included with this book—your OpenLinux CD-ROM, which is a working archive of nearly all the software used in this book. If you carefully preserve your /home and /etc directories, you can recover from a hard drive disaster to a working system within minutes.

## Exercises

- 1. Use the tar command to create a compressed archive of your /etc and /home directories. How large is the file?
- 2. Use the du command to estimate the size of your OpenLinux system. How else can you find out how much space is required?
- 3. Investigate ways to prepare for a hard drive disaster. If your hard drive crashes, what files do you most fear losing? What steps can you take to prevent losing these files?

## Hour 24

### Using Scheduling to Automate System Management

In this hour, you'll finish by learning basic system administration skills. By now you know most of the commands used by sysadmins and are familiar with most of the tasks you have to perform to maintain your system for yourself or other users. This hour shows you how to put all this knowledge together in order to automate these tasks using the cron daemon and other OpenLinux scheduling programs.

By using the programs and techniques outlined in this hour, you can automate many different system administration jobs and maintain a healthy, well-running system. The first topic is the cron daemon, and then you'll learn how to administer the at command facilities for different users on your system.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_544_0.png)
