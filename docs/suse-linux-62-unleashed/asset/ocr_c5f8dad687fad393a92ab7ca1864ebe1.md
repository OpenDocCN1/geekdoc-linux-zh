The advantage of this backup scheme is that it requires only two sets of backup media. Restoring the full system from the level 0 backup and the previous evening's incremental can perform a complete restore. The negative side is that the amount backed up grows throughout the week, and additional media might be needed to perform the backup. The following is the second strategy:

+   * Sunday Level 0 backup
* Monday Level 1 backup
* Tuesday Level 2 backup
* Wednesday Level 3 backup
* Thursday Level 4 backup
* Friday Level 5 backup
* Saturday Level 6 backup

The advantage of this backup scheme is that each backup is relatively quick. Also, the backups stay relatively small and easy to manage. The disadvantage is that it requires seven sets of media. Also, you must use all seven sets to do a complete restore.

When deciding which type of backup scheme to use, you need to know how the system is used. Files that change often should be backed up more often than files that rarely change. Some directories, such as /tmp, never need to be backed up.

# # Performing Backups with tar and cpio

A full backup with tar is as easy as

```
$ tar c /
```

An incremental backup takes a bit more work. Fortunately, the find command is a wonderful tool to find all files that have changed since a certain date. It can also find files that are newer than a specified file. With this information, it is easy to perform an incremental backup. The following command finds all files that have been modified today in the current directory and backs up those files with the tar command to perform an archive on /dev/rmt1

```
$ find -mtime 1 ! -type d | tar cf >/dev/rmt1
```

The ! -type shows that if the object is a directory, don't give it to the tar command for archiving. This is done because tar follows the directories, and you don't want to back an entire directory unless it has changed. Of course, the find command can also be used for the cpio command. The following command performs the same task as the preceding tar command:

```
$ find -mtime 1 | cpio -o >/dev/rmt1
```

![](bbox=[0.865, 0.797, 0.98, 0.963])