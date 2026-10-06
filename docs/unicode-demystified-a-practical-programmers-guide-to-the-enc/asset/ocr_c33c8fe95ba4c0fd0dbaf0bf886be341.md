```
# cd /
# find . -depth 1 cpio > /dev/st0
```

The following command restores all the files in the /home directory from the preceding backup. The options extract files from an archive (-i) in verbose mode, keeping the modification times and directories as needed.

```
# cd /
# cpio -ivd /home/* < /dev/st0
```

# Exclude Some Directories from a Backup

In practice you exclude some directories from the backup process. For example, not backing up /tmp or /var/tmp (or its link, /usr/tmp) can save room in the archive. Also, do not back up the files in /proc because the /proc filesystem is not a disk filesystem but rather a way for the Linux kernel to provide with information about operating and system memory, you need not back up /proc; you cannot restore it. You do not need to back up filesystems that are mounted on other computers in your network. Do not back up FIFOs: the results are unpredictable. If you plan on using a simple method, similar to those just shown, create a file naming the directories to exclude from the backup, and use the appropriate option with the archive program.

Although any of the archive programs works well for such simple backups, only amanda has the support to provide a sophisticated backup and restore system. For example, to determine whether a file is in an archive requires you to read the entire archive. If the archive is split across several tapes, this is particularly tiresome. More sophisticated utilities, including amanda, assist you in several ways, including keeping a table of contents of the files in a backup.

# dump, restore: Back Up and Restore Filesystems

The dump utility, first seen in UNIX version 6, backs up an entire filesystem, or only those files that have changed since the last dump. The restore utility restores an entire filesystem, an individual file, or a piece of the filesystem hierarchy (a directory and its descendants). You will get the best results if you perform a backup on a quiescent system so that the files are not changing as you make the backup.

The following command performs a complete backup of all files (including directories and special files) on the root (/) partition onto SCSI tape 0:28

> 28. Frequently there is a link to the active tape drive, named /dev/tape, which you can use in place of the actual entry in the /dev directory.