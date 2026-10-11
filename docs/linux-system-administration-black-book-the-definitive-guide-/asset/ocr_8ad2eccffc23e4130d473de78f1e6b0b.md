# Introduction To Backup Schemes

There are a variety of backup schemes you can use. A backup scheme is a reference to your backup approach. There are a number of issues that affect how you determine what your backup scheme will ultimately be.

# Portion Of File System

Take a look at how easy each portion of the file system is to re-create. Be careful how you determine whether something is simple or not—what may seem simple now may not seem so easy five months later when you need to fix things after a crash.

It is possible to back up the entire file system if you have media large enough to hold it, or if you can span it among multiple media. However, as you will learn in the two sections on incremental backups in this chapter's Immediate Solutions section, it is not necessary to back up the entire file system every time. Items that administrators commonly back up most frequently are:

+   - The /home hierarchy
+   	- Hierarchies that contain file server data, such as FTP or Web server file storage areas
+   	- Any special directories containing program data
+   	- Log files with data you cannot afford to lose, such as Web access data
+   	- The /etc hierarchy, if you have configured many services lately

# Frequency

The frequency with which you make backups depends on your particular situation. You do not need to back up all items at the same frequency. Instead, you can have a separate backup set up for each important portion of the file system.

The main indicator of how often you need to back up a file system segment is how often the data changes, and how much of a problem it would be to lose data that is not yet backed up if a crash happens. If a month will not make much of a difference due to part of the hierarchy being fairly static, and the information there is not difficult to re-create, then that portion would not need to be backed up often. However, for data that can change at any moment and frequently—such as home directories and mail spools—a daily backup is highly recommended.

# Redundancy

If you keep one set of backup media and write over the media each time you back up, you miss out on the issue of redundancy. Perhaps an intruder crept in and you were unaware of him or her for a week. Those daily backups may contain corrupted files, and you have no way of checking them against anything older. This is



![](bbox=[0.92, 0.25, 0.98, 0.42])