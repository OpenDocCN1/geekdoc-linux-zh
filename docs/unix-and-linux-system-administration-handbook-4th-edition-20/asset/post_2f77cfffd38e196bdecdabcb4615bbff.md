
# Restoring from dumps restore

When you are notified of a lost file, first determine which tapes contain versions of the file. Users often want the most recent version, but that is not always the case. For example, a user who loses a file by inadvertently copying another file on top of it would want the version that existed before the incident occurred. It is helpful if you can browbeat users into telling you not what files are missing but also when they were lost and when they were last modified. We find helpful to structure users' responses with a request form.

If you do not know on-line catalogs, you must mount tapes and repeatedly attempt to restore the missing files until you find the correct tape. If the user remembers when the files were last changed, you might be able to make an educated guess about which tapes the files might be on.

After determining which tapes you want to extract, create and cd to a temporary directory such as /var/restore where a large directory hierarchy is created; most versions of restore must create all the directories leading to a particular file before that file can be restored. Do not use /tmp—your work could be wiped out if the machine crashes and reboots the restored data has

The restore command has many options. Most useful are -i for interactive stores of individual files and directories and -r for a complete restore of an entire filesystem. You might also need -x, which requests a noninteractive restore of specified files—be careful not to overwrite existing files.

restore - reads the contents of the tape and then lets you navigate through as you would a normal directory tree, using commands ls, cd, and pwd. You mark the files that you want to restore with the add command. When you finish selecting, use extract to pull the files off the tape.

If you placed multiple dumps on a single tape, you must use the mt command to position the tape at the correct dump file before running restore. Remember to use the non-rewinding device!

For example, to restore the file /users/janet/iam_rost from a remote tape drive, you might issue the following commands. Let's assume you have found the right tape, mounted on tapehost:/dev/nst0, and determined that the filesystem containing janet's directory is fourth on the tape.

```
$ mkdir /var/restore
$ cd /var/restore
$ ssh tapehost mt -f /dev/nst0 fsf 3
$ restore -i f tapehost:/dev/nst0
restore> ls
janet/ garth/ lost+found/ lynda/
restore> cd janet
restore> ls
afile bfile chile iam_rost
```

Page 317 for a description of mt.

![](img/579efec8c67772f31ecf34844bbb71a2_359_0.png)

# Chapter 10 Backups

```
restore> add iam_last
restore> ls -l
afile bfile cfile iam_last*
restore> extract
```

You have not read any volumes yet. Unless you know which volume your files are on you start with the last volume and work towards the first. Specify volume # 1.
set owner/mode for '?' [yn] n

Volumes (tapes) are enumerated starting at 1, not 0, so for a dump that is on single tape, you specify 1. When restore asks if you want to set the owner and mode, it is asking whether it should set the current directory to the root of the tape. If you are restoring an entire filesystem, you probably do not want to this.

Once the restore has completed, give the file to janet:

```
$ cd /var/restore
$ ls jane/iam_last
$ ls -jane_last
afile bfile
$ sudo cp -p jane/iam_last -jane/iam_last.restored
$ sudo chown staff -jane/iam_last.restored
$ sudo chgrp staff -jane/iam_last.restored
$ cd /; sudo rm -rf /var/restore
$ mail jane
```

Your file iam_last has been restored as requested and has been placed in /users/jane/iam_last.restored.

Your name, Humble System Administrator

Some administrators prefer to restore files into a special directory and allow users to copy their files out by hand. In that scheme, the administrator must protect the priv of the restored files by verifying their ownership and permissions. If you choose to use such a system, remember to clean out the directory often.

If you originally wrote a backup to a remote tape drive and are unable to restore files from locally, however, try to host it on the same remote host that was used for the original backup.

restore -i is usually the easiest way to restore a few files or directories from a dump, it does not work if the tape device cannot be moved backwards a record at a time (a problem with some 8mm drives). If restore -i fails, try restore -x before jumping out the window. restore -x requires you to specify the complete path of the file you want to restore (relative to the root of the dump) on the command line. The following sequence of commands repeats the previous example, with -x.

The next to -x iam_last indicates that it has been marked for extraction.

# Restoring entire filesystems

```
$ sudo mkdir /var/restore
$ cd /var/restore
$ sudo ssh tapehost mt -f /dev/nst0 fsf 3
$ sudo restore -x tapehost:/dev/nst0 /janet/iam_lost
```

# Restoring entire filesystems

With luck, you will never have to restore an entire filesystem after a system failure. However, the situation does occasionally arise. Before attempting to restore the filesystem, be absolutely sure that whatever problem caused the filesystem to be destroyed in the first place has been taken care of. It's pointless to spend hours spinning tapes only to load the filesystem once again.

Before you begin a full restore, create and mount the target filesystem. Chapter 8, Storage, for more information about how to prepare the filesystem. To start the restore, cd to the mount point of the new filesystem, put the first tape of the most recent level 0 dump in the tape drive, and type restore -r.

restore prompts for each tape in the dump. After the level 0 dump has been restored, mount and restore the incremental dumps. Restore incremental dumps, in the order in which they were created. Because of redundancy among dumps, it may not be necessary to restore every incremental. Here's the algorithm for determining which dumps to restore:

- Step 1: Restore the most recent level 0 dump.
- Step 2: Restore the lowest-level dump made after the dump you restored. If multiple dumps were made at that level, restore the most recent one.
- Step 3: If that was the last dump, you are done.
- Step 4: Otherwise, go back to step 2.

The next to -x iam_last indicates that it has been marked for extraction.

```
$ sudo mkdir /var/restore
$ cd /var/restore
$ sudo ssh tapehost mt -f /dev/nst0 fsf 3
$ sudo restore -x tapehost:/dev/nst0 /janet/iam_lost
```

# Restoring entire filesystems

With luck, you will never have to restore an entire filesystem after a system failure. However, the situation does occasionally arise. Before attempting to restore the filesystem, be absolutely sure that whatever problem caused the filesystem to be destroyed in the first place has been taken care of. It's pointless to spend hours spinning tapes only to load the filesystem once again.

Before you begin a full restore, create and mount the target filesystem. Chapter 8, Storage, for more information about how to prepare the filesystem. To start the restore, cd to the mount point of the new filesystem, put the first tape of the most recent level 0 dump in the tape drive, and type restore -r.

restore prompts for each tape in the dump. After the level 0 dump has been restored, mount and restore the incremental dumps. Restore incremental dumps, in the order in which they were created. Because of redundancy among dumps, it may not be necessary to restore every incremental. Here's the algorithm for determining which dumps to restore:

- Step 1: Restore the most recent level 0 dump.
- Step 2: Restore the lowest-level dump made after the dump you restored. If multiple dumps were made at that level, restore the most recent one.
- Step 3: If that was the last dump, you are done.
- Step 4: Otherwise, go back to step 2.

The next to -x iam_last indicates that it has been marked for extraction.

```
$ sudo mkdir /var/restore
$ cd /var/restore
$ sudo ssh tapehost mt -f /dev/nst0 fsf 3
$ sudo restore -x tapehost:/dev/nst0 /janet/iam_lost
```

# Restoring entire filesystems

With luck, you will never have to restore an entire filesystem after a system failure. However, the situation does occasionally arise. Before attempting to restore the filesystem, be absolutely sure that whatever problem caused the filesystem to be destroyed in the first place has been taken care of. It's pointless to spend hours spinning tapes only to load the filesystem once again.

Before you begin a full restore, create and mount the target filesystem. Chapter 8, Storage, for more information about how to prepare the filesystem. To start the restore, cd to the mount point of the new filesystem, put the first tape of the most recent level 0 dump in the tape drive, and type restore -r.

restore prompts for each tape in the dump. After the level 0 dump has been restored, mount and restore the incremental dumps. Restore incremental dumps, in the order in which they were created. Because of redundancy among dumps, it may not be necessary to restore every incremental. Here's the algorithm for determining which dumps to restore:

- Step 1: Restore the most recent level 0 dump.
- Step 2: Restore the lowest-level dump made after the dump you restored. If multiple dumps were made at that level, restore the most recent one.
- Step 3: If that was the last dump, you are done.
- Step 4: Otherwise, go back to step 2.

The next to -x iam_last indicates that it has been marked for extraction.

```
$ sudo mkdir /var/restore
$ cd /var/restore
$ sudo ssh tapehost mt -f /dev/nst0 fsf 3
$ sudo restore -x tapehost:/dev/nst0 /janet/iam_lost
```

# Restoring entire filesystems

With luck, you will never have to restore an entire filesystem after a system failure. However, the situation does occasionally arise. Before attempting to restore the filesystem, be absolutely sure that whatever problem caused the filesystem to be destroyed in the first place has been taken care of. It's pointless to spend hours spinning tapes only to load the filesystem once again.

Before you begin a full restore, create and mount the target filesystem. Chapter 8, Storage, for more information about how to prepare the filesystem. To start the restore, cd to the mount point of the new filesystem, put the first tape of the most recent level 0 dump in the tape drive, and type restore -r.

restore prompts for each tape in the dump. After the level 0 dump has been restored, mount and restore the incremental dumps. Restore incremental dumps, in the order in which they were created. Because of redundancy among dumps, it may not be necessary to restore every incremental. Here's the algorithm for determining determining dumps to restore:

- Step 1: Restore the most recent level 0 dump.
- Step 2: Restore the lowest-level dump made after the dump you restored. If multiple dumps were made at that level, restore the most recent one.
- Step 3: If that was the last dump, you are done.
- Step 4: Otherwise, go back to step 2.

The next to -x iam_last indicates that it has been marked for extraction.

```
$ sudo mkdir /var/restore
$ cd /var/restore
$ sudo ssh tapehost mt -f /dev/nst0 fsf 3
$ sudo restore -x tapehost:/dev/nst0 /janet/iam_lost
```

# Restoring entire filesystems

With luck, you will never have to restore an entire filesystem after a system failure. However, the situation does occasionally arise. Before attempting to restore the filesystem, be absolutely sure that whatever problem caused the filesystem to be destroyed in the first place has been taken care of. It's pointless to spend hours spinning tapes only to load the filesystem once again.

Before you begin a full restore, create and mount the target filesystem. Chapter 8, Storage, for more information about how to prepare the filesystem. To start the restore, cd to the mount point of the new filesystem, put the first tape of the most recent level 0 dump in the tape drive, and type restore -r.

restore prompts for each tape in the dump. After the level 0 dump has been restored, mount and restore the incremental dumps. Restore incremental dumps, in the order in which they were created. Because of redundancy among dumps, it may not be necessary to restore every incremental. Here's the algorithm for determining which dumps to restore:

- Step 1: Restore the most recent level 0 dump.
- Step 2: Restore the lowest-level dump made after the dump you restored. If multiple dumps were made at that level, restore the most recent one.
- Step 3: If that was the last dump, you are done.
- Step 4: Otherwise, go back to step 2.

The next to -x iam_last indicates that it has been marked for extraction.

```
$ sudo mkdir /var/restore
$ cd /var/restore
$ sudo ssh tapehost mt -f /dev/nst0 fsf 3
$ sudo restore -x tapehost:/dev/nst0 /janet/iam_lost
```

# 10.5 DUMPING AND RESTORING FOR UPGRADES

We recommend that when you perform a major OS upgrade, you back up all filesystems with a level 0 dump and, possibly, restore them. The restore is needed if the new OS uses a different filesystem format or if you restructure your disks. However, you must back as insurance against any problems that might occur during the upgrade. A complete set of backups also gives you the option to retain the old OS if the new version does not prove satisfactory. Fortunately, with the progressive upgrade systems used by most distributions these days, you are unlikely to need these tapes.

Be sure to back up system and user partitions. Depending on your upgrade path, you may choose to restore only user data and system-specific files that are in the root filesystem or in /usr, such as /etc/passwd, /etc/shadow, or /usr/local. UNIX directory organization mixes local files with vendor-distributed files, making it quite difficult to pick out your local customizations.

# Restoring to new hardware

When an entire system has failed, you must perform what is known as "bare metal recovery." Before you follow the filesystem restoration steps above, you will at need to

- Provision replacement hardware
- Install a fresh copy of the operating system
- Install backup software (such as dump and restore)
- Configure the local tape drive or configure access to a tape server

After these steps, you can follow the restoration process described above.
