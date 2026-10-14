If you want to perform a hot backup on an application that has constantly open files, the application must have a hot backup feature, and the backup software needs hot backup support for the specific application. Generally speaking, in hot backup mode, instead of writing to the live data, the application queues up the updates in a special file so the backup software can get a complete backup of the database. The special file is backed up next. After this is done, the application is then allowed to apply the queued-up changes to the database, thus bringing everything up to date.

Therefore, to decide whether you should perform a cold or hot backup of your database application files, you need to take the following factors into consideration:

+   - Can the application data files be backed up cold and not violate their integrity? If not, does the application have a hot backup feature?
+   - Does your backup software support the hot backup option of that particular application?
+   - How much of a downtime window do you have to back up this application's data files? Perhaps the window is wide enough for a cold backup, which would make life a lot easier.

If you have small downtime window but have sufficient disk space, perhaps using the Logical Volume snapshot feature is an option.

# # Backup and Restore Tools

There are a variety of methods of performing backups with SLES. They include the general-purpose command-line tools included with every Linux distribution, such as tar, dd, dump, and cpio. Newer Linux distributions, such as SLES 9, include some text-based utilities, such as AMANDA (Advanced Maryland Automatic Network Disk Archiver) and taper. These utilities are designed to add a more user-friendly interface to the backup and restore procedures. GUI-based utilities are available as well, such as the System Backup and Restore modules in YaST. Finally, many commercial backup utilities are also available, such as BRU, CTAR, ARCserve, Legato NetWorker, and System Backup Administrator. Any one of these backup solutions can provide protection for your valuable data.

# **CAUTION**

When you are selecting a backup utility, ensure it supports the filesystem types that you are using. For instance, Legato NetWorker 7.2 for Linux supports ext2/ext3, ReiserFS, and JFS (Journaled File System), but not XFS.