
tar or Lone-Tar, which is a great advantage if you are moving your backup media to another machine.

The amount of time required to make a backup depends on a number of factors, most importantly the size of the filesystem, the speed of your backup system, and the load on your system. If you have a fast system and a high-capacity fast backup device, Lone-Tar backs up your system much faster than tar itself would have. However, the speed is most limited by the backup devices themselves. A DAT SCSI drive, for example, is much faster than a QIC cartridge tape drive driven off the floppy. You will get used to the amount of time required for a master backup after a couple of backup cycles. If there's a long time required, start scheduling the backups at night while you sleep, or when you go away for a reasonable period of time. Take note that most master backups take at least an hour and often many hours, depending on the backup drives.

> **TIP**
> Make sure you label the tape or other medium with the date and type of backup. Write clearly! You never know when you'll have to figure out which tape was made when.

To make an incremental backup, follow the same process. Since most incremental backups are much smaller than a master backup, they also back up much faster. You really should get in the habit of making incremental backups either every day you use the Linux system, or whenever you save something you really can't afford to lose. It's better to spend ten minutes making a backup than four hours rewriting that chapter of your latest book!

A selective backup, started using the S option on the Lone-Tar menu, lets you back up only specific areas of your system. You are asked which files or directories to include or exclude, then the backup proceeds normally.

### Verifying Files

The Verify option provided by Lone-Tar is a security precaution that you should make use of every time you make a backup. The Verify option scans through the backup and compares it to the original files. This makes sure that any backup errors are caught before they become serious.

It is a good habit to get into verifying each backup after it has been made. This is especially true when you have made new master backups.

Remember that some files on your system may change between the backup time and the verification time, depending on whether the system was used between the two times or not. Some automated procedures such as mail, logging, news, and automated background tasks alter files while a backup or verification is proceeding. Lone-Tar finds the files different and reports errors to you. You should carefully read the reports from the Verification process so you know which errors are important and which occurred because of these system changes.

### Restoring Files

When you have to restore a file, directory, or entire filesystem, find the proper backups. If you have been using the master and incremental routine, you will need the last master and all the incrementals since that master. Alternatively, if you are just looking for a few files you accidentally deleted, you may know which tape or drive they are on and can use just that medium.

To start a restore process, select the **R** option from the Lone-Tar main menu. This brings up the Restore menu, shown in Figure 64.7. Most of the options on the Restore menu are self-descriptive. For example, to restore an entire tape, you would use the “Restore entire tape to hard disk” option.

![](img/e8e6b47ac20475e23d48b4c476f5d891_1053_0.png)

Some of the other options on the Restore menu enable you to selectively restore directories or files, based on exact names or wildcards. You can also build a list of files or directories and have them all restored at once. Alternatively, you can decide which files or directories are not to be restored, create an exclusion list of them, and restore everything else.

After you have decided which files or directories to restore, Lone-Tar asks you to insert the tape and starts the restoration process. As with a backup, Lone-Tar echoes everything it does to the screen so you can see what it is doing.

> **Tip**
> When performing a restore of a few files or directories, Lone-Tar has to search through the tape or medium to find those files. This can be a slow process, depending on the speed of the backup device, so don't worry if you don't see anything happening for a few minutes. You should see the status lights on your backup device blinking to show the device is being used by Lone-Tar.

If there is more than one tape or other device involved in the backup, Lone-Tar prompts you to insert the next volume. It keeps doing so until the restore process is complete.

If you are restoring from a combination of masters and incrementals, you must repeat the restore process for each tape. For example, if you accidentally erased an entire directory, you could use the last master backup to get the main files and then go through all the incrementals made since the master was created to obtain any changes. You have to perform the updates manually by using the Restore menu.

After the restoration is completed, Lone-Tar returns to the main menu. You should verify that the backup was to the proper location and everything looks correct.

Tape-Tell is a special feature of Lone-Tar that tells you a little about when the tape was used. This hinges on the Lone-Tar file that can be put at the beginning of the medium. We discussed this file in the section above on backing up using Lone-Tar.

## Utilities and Environment: Tweaking Lone-Tar

The Lone-Tar Utilities menu, shown in Figure 64.8, holds a number of useful commands and functions. Most of these options are self-explanatory, but a few are very handy for users. It is helpful to check the backup date of the last master backup occasionally as a reminder of when you should start thinking about a new master backup.

The automated use of Lone-Tar through cron is a neat feature that lets your system make backups without you being there. As you know from earlier chapters in this book, cron lets you schedule commands to be run at particular times or intervals, so you can easily set Lone-Tar to be run by cron to create incremental backups every night, twice a week, or whenever you want. You don't need to know details about cron in order to schedule backups; Lone-Tar takes care of that for you.

### FIGURE 64.8.

The Lone-Tar
Utilities menu.

![](img/e8e6b47ac20475e23d48b4c476f5d891_1055_0.png)

The Utilities menu also lets you change the backup device type and details, so if you have more than one backup system on your Linux system, you can change between them. This is useful if you want to make master backups to a high-capacity device but incrementals to a different device.

The Environment menu, shown in Figure 64.9, contains a list of all the settings Lone-Tar works with. Many of these were set when you installed Lone-Tar, but you can modify them as you need in order to customize your installation.

### FIGURE 64.9.

The Lone-Tar
Environment
menu lets you
alter the behavior
of the backup tool.

![](img/e8e6b47ac20475e23d48b4c476f5d891_1055_1.png)

## Summary

Lone-Tar has a lot of features we haven't mentioned in this chapter, but you can read the online documentation to find out more about the system. Using Lone-Tar for your backup and restore operations is fast and easy, and you'll find yourself doing them a lot more when you don't have to fumble with awkward syntax or worry about mistyping a command. You should try to use the Lone-Tar demo we've provided on the CD-ROM. You'll find it very easy to work with. From here there are a number of chapters you might be interested in:

- To learn more about mounting devices such as floppy disks and CD-ROMs, see Chapter 33, “Devices.”
- To learn more about backups and making sure your system is completely covered in case of problems, see Chapter 45, “Backups.”
- To learn more about automating your backups at night, see Chapter 46, “cron and at.”
