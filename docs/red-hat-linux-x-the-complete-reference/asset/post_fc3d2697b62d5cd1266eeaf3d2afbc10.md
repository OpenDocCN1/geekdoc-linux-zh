
## Backups

You can back up and restore your system archive tools like tar, restoring the archives later. For backups, tar is usually used with a tape device. To automatically schedule backups, you can schedule appropriate tar commands with the cron utility.

## Amanda

To back up hosts connected to a network, you can use the Advanced Maryland Automatic Network Disk Archiver (Amanda) to archive hosts. Amanda uses tar tools to back up all hosts to a single host operating as a backup server. Backup data is sent by each host to the host operating as the Amanda server, where they are written out to a backup medium such as tape. With an Amanda server, the backup operations for all hosts become centralized in one server, instead of each host having to perform its own backup. Any host that needs to restore data simply requests it from the Amanda server, specifying the file system, date, and file names. Amanda has its own commands corresponding to the common backup tasks, beginning with "am", such as amdump, amrestore, and amrecover. Configuration files are placed in /etc/amanda and log, and database files in /var/adm/amanda.

## Backups with dump and restore

You can back up and restore your system with the dump and restore utilities. dump can back up your entire system or perform incremental backups, saving only those files that have changed since the last backup. dump supports several options for managing the backup operation, such as specifying the size and length of storage media (see Table 27-11).

## dump Levels

dump uses dump levels to determine to what degree you want your system backed up. A dump level of 0 will copy file systems in their entirety. The remaining dump levels perform incremental backups, backing up only files and directories that have been created or modified since the last lower-level backup. A dump level of 1 will back up only files that have changed since the last level 0 backup. The dump level 2, in turn, will back up only files that have changed since the last level 1 backup (or 0 if there is no level 1), and so on up to dump level 9. You could run an initial complete backup at dump level 0 to back up your entire system, and then run incremental backups at certain later dates, having to back up only the changes since the full backup.

Using dump levels, you can devise certain strategies for backing up a file system. It is important to keep in mind that an incremental backup is run on changes from the last lower-level backup. For example, if the last backup was 6 and the next backup was 8, then the level 8 would back up everything from the level 6 backup. The sequence of the backups is important. If there were three backups with levels 3, then 6, and then 5, the level 5 backup would take everything from the level 3 backup, not stopping at level 6. Level 3 is the next lower-level backup for level 5, in this case. This can make for some complex incremental backup strategies. For example, if you want each succeeding incremental backup to include all the changes from the preceding incremental backups, you could run the backups in descending dump level order. Given a backup sequence of 7, 6, and 5, with 0 as the initial full backup, 6 would include all the changes to 7, because its next lower level is 0, making level 0. Then 5 would include all the changes for 7 and 6, also because its next lower level is 0, making all the changes since the level 0 full backup. A simpler way to implement this is to make the incremental levels all the same. Given an initial level of 0, and then two backups both with level 1, the last level 1 would include all the changes from the backup with level 0, since level 0 is the next lower level-not the previous level 1 backup.

## Recording Backups

Backups are recorded in the /etc/dumpdates file. This file will list all the previous backups, specifying the file system they were performed on, the dates they were performed, and the dump level used. You can use this information to restore files from a specified backup. Recall that the /etc/fstab file records the dump level as well as the recommended backup frequency for each file system. With the -f option, dump will analyze both the /etc/dumpdates and /etc/fstab files to determine which file systems need to be backed up. The dump command with the -w option just uses /etc/fstab to report the file systems ready for backup.

### Table 27-11: dump Options

| Options | Description |
|---|---|
| -0 through -9 | Specifies the dump level. A dump level 0 is a full backup, copying the entire file system (see also the -h option). Dump level numbers above 0 perform incremental backups, copying all new or modified files new in the file system since the last backup at a lower level. The default level is 9. |
| -B records | Lets you specify the number of blocks in a volume, overriding the end-of-media detection or length and density calculations that dump normally uses for multivolume dumps. |
| -a | Lets dump bypass any tape length calculations and write until an end-of-media indication is detected. Recommended for most modern tape drives and is the default. |
| -b blocksize | Lets you specify the number of kilobytes per dump record. With this option, you can create larger blocks, speeding up backups. |
| -d density | Specifies the density for a tape in bits per inch (default is 1,600 BPI). |
| -h level | Files that are tagged with a user's nodump flag will not be backed up at or above this specified level. The default is 1, which will not back up the tagged files in incremental backups. |
| -f file/device | Backs up the file system to the specified file or device. This can be a file or tape drive. You can specify multiple filenames, separated by commas. A remote device or file can be referenced with a preceding hostname, hostname:file. |
| -k | Uses Kerberos authentication to talk to remote tape servers. |
| -M file/device | Implements a multivolume backup, where the file written to is treated as a prefix and the suffix consisting of a numbered sequence from 001 is used for each succeeding file, file001, file002, etc. Useful when backup files need to be greater than the Linux ext3 2GB file size limit. |
| -n | Notifies operators if a backup needs operator attention. |
| -s feet | Specifies the length of a tape in feet. dump will prompt for a new tape when the length is reached. |
| -S | Estimates the amount of space needed to perform a backup. |
| -u | Writes an entry for a successful update in the /etc/dumpdates file. |
| -W | Detects and displays the file systems that need to be backed up. This information is taken from the /etc/dumpdates and /etc/fstab files. |
| -w | Detects and displays the file systems that need to be backed up, drawing only on information in /etc/fstab. |

## dump Operation

The dump command takes as its arguments the dump level, the device it is storing the backup on, and the device name of the file system that is being backed up. If the storage medium (such as a tape) is too small to accommodate the backup, dump will pause and let you insert another. dump supports backups on multiple volumes. The **u** option will record the backup in the **/etc/dumpdates** file. In the following example, an entire backup (dump level 0) is performed on the file system on the **/dev/hda3** hard disk partition. The backup is stored on a tape device, **/dev/tape**.

```
dump -0u -f /dev/tape /dev/hda5
```

Note You can use the mt command to control your tape device. mt has options to rewind, erase, and position the tape. The rmt command controls a remote tape device.

The storage device can be another hard disk partition, but it is usually a tape device. When you installed your system, your system most likely detected the device and set up /dev/tape as a link to it (just as it did with your CD-ROMs). If the link was not set up, you have to create it yourself or use the device name directly. Tape devices can have different device names, depending on the model or interface. SCSI tape devices are labeled with the prefix st, with a number attached for the particular device. st0 is the first SCSI tape device. To use it in the dump command, just specify its name.

```
dump -0u -f /dev/st0 /dev/hda5
```

Should you need to back up to a device located on another system on your network, you would have to specify that hostname for the system and the name of its device. The hostname is entered before the device name and delimited with a colon. In the following example, the user backs up file system /dev/hda5 to the SCSI tape device with the name /dev/st0 on the rabbit.mytrek.com system:

```
dump -0u -f rabbit.mytrek.com:/dev/st0 /dev/hda5
```

The dump command works on one file system at a time. If your system has more than one file system, you will need to issue a separate dump command for each.

Tip You can use the system **cron** utility to schedule backups using dump at specified times.

## Recovering Backups

You use the restore command to either restore an entire file system or to just retrieve particular files. restore will extract files or directories from a backup archive and copy them to the current working directory. Make sure you are in the directory you want the files restored to when you run restore. restore will also generate any subdirectories as needed. restore has several options for managing the restore operation (see Table 27-12).
