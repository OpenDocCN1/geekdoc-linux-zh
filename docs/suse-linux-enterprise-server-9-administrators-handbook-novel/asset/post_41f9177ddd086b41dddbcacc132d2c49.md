
## TABLE 10.7
**Noteworthy dump Command-Line Options (continued)**

| OPTION | DESCRIPTION |
|---|---|
| `-f file` | Tells dump where the dump image goes. It defaults to `/dev/tape`, and it also checks to see what the TAPE environment variable is set to if no `/dev/tape` exists. This option is useful if you would like to send the dump to a remote device (`/dev/rmt/?`), a file on the local filesystem (or an NFS mount), or pipe the results back to standard input. Output to stdout, specify a filename of `-`. |
| `-L label` | Specifies a label for the dump image. Unfortunately, you have only 16 characters to work with here, so you need to be careful what you use. One suggestion is to use the device name (such as a label of `/dev/sda6`). |
| `-q` | Makes dump abort immediately if it encounters a situation that would normally require user input. This option is useful for scripting automated backups because dump reads its input straight from the tty instead of from stdin, which prevents you from using something like `yes no | dump -0au /dev/hda1` in your script. This option did not appear in dump until version 0.4b24. |
| `-u` | This option is very important if you are planning to make incremental backups of a filesystem. This option tells dump to update the `/etc/dumpdates` file, which essentially records the date and time you ran the dump and the level the dump was set to run at. If you forget this, you will continuously be doing full level (level 0) backups. |
| `-z[compression_level]` | Compresses every block to be written on the tape using the zlib library. This option works only when dumping to a file or pipe or when outputting to a tape drive if the tape drive is capable of writing variable length blocks. The (optional) parameter specifies the compression level zlib will use. The default compression level is 2. If the optional parameter is specified, there must be no whitespace between the option letter and the parameter—for example, `-z3`. You need at least the 0.4b22 version of restore to extract compressed tapes. Tapes written using compression are not compatible with the BSD tape format. |

## NOTE
dump sends all of its output through stderr, so a command such as the following is valid:

```
dump -0af /tmp/backup /home 2>/tmp/backup.log
```

This example sends the dump image to /tmp/backup and causes the stderr output from dump to go to /tmp/backup.log.

Running dump may seem complicated, but it is actually fairly straightforward. A typical command looks like this:

```
Athena:~ # dump -0a -L “/dev/hda1: /boot” -f /dev/st0 /boot
```

When dump is invoked normally, backup proceeds with some messages printed on the console, as shown in Listing 10.1. It is a good idea to leave this session in the foreground rather than send it to the background until you are convinced everything works fine. If dump reaches the end of tape or if some error occurs, you will be requested to make some choices in the interactive session.

## LISTING 10.1
Sample dump Log Messages

```
DUMP: Date of this level 0 dump: Sat Jan 29 17:03:55 2005
DUMP: Dumping /dev/hda1 (/boot) to /dev/st0
DUMP: Added inode 21 to exclude list (Journal inode)
DUMP: Label: /dev/hda1: /boot
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 11000 tape blocks.
DUMP: Volume 1 started with block 1 at:
Sat Jan 29 17:03:55 2005
DUMP: dumping (Pass II) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/st0
DUMP: Volume 1 completed at: Sat Jan 29 17:03:56 2005
DUMP: Volume 1 10940 tape blocks (10.68MB)
DUMP: Volume 1 took 00:00:01
DUMP: Volume 1 transfer rate: 10940 KB/s
DUMP: 10940 tape blocks (10.68MB) on 1 volume(s)
DUMP: finished in 1 seconds, throughput 10940 KBytes/sec
DUMP: Date of this level 0 dump: Sat Jan 29 17:03:55 2005
DUMP: Date this dump completed: Sat Jan 29 17:03:56 2005
DUMP: Average transfer rate: 10940 kB/s
DUMP: DUMP IS DONE
```

The log messages in Listing 10.1 also indicate whether any files (inodes) are skipped. In the example, the log shows inode 21 was excluded from the backup. The reason is that inode 21 turns out to be the journal for the ext3 filesystem; therefore, it does not need to be backed up and can be excluded from future backups.

When the dump session finishes properly, you can dump another filesystem if enough tape capacity remains.

## TIP
It is always a good idea to first check the filesystem's integrity prior to doing a dump, especially when it is a full dump. To do this, after you have entered single-user mode, unmount the filesystems one by one and check them using e2fsck:

```
Athena: # umount /usr/home; e2fsck -afv /dev/sdd1
```

Check all the filesystems that are to be backed up, preferably after unmounting them. Because you cannot unmount the root filesystem, you may want to remount it as read-only to prevent its data (thus the inodes) from being modified and check it with e2fsck:

```
Athena: # mount -n -o remount / ; e2fsck -afv /dev/hda1
```

After all the checks are done, remount it again with read-write so that dump can log the backup information:

```
Athena: # mount -w -n -o remount /
```

A simple incremental backup strategy is shown in Table 10.8.

## TABLE 10.8
*A Simple Incremental Backup Strategy Using dump*

| DAY | DUMP LEVEL |
|---|---|
| Day 1 | Level 0 |
| Day 2 | Level 1 |
| Day 3 | Level 2 |
| Day 4 | Level 3 |
| Day 5 | Level 4 |
| Day 6 | Level 5 |
| Day 7 | Level 6 |
| Day 8 | Level 7 |
| Day 9 | Level 8 |
| Day 10 | Level 9 |
| Day 11 | Level 0 (and the sequence repeats) |

After Day 2, dump backs up updated files only. And on Day 11, you make a complete backup again and the sequence repeats.

Some people use a more elaborate method, using the Tower of Hanoi sequence, for the dump-level scheduling. This method may employ the following sample sequences:

```
Rotation 1: 0, 3, 2, 5, 4, 7, 6, 9, 8
Rotation 2: 1, 3, 2, 5, 4, 7, 6, 9, 8
Rotation 3: 1, 3, 2, 5, 4, 7, 6, 9, 8
```

In this case, you start with a level 0 dump and then perform daily incremental backups based on the sequence. The pattern repeats itself after 27 days.

Note that under this scenario, each level 0 dump should be made on a new tape and stored at a safe place. For level 1 backups, use two different tapes (or as many as the number of rotations). For other dump levels, one tape per level is sufficient, and they can be reused from one rotation to another.

## CAUTION
> If you are considering the Tower of Hanoi sequence for your dump-level schedule, pay attention to the section “A Few Words of Caution About Dump Levels” later in this chapter.

## RECOVERING DATA USING restore
There are two main methods of restoring files from a dump archive: either interactively (when the -i switch is specified) or through a full restore. You point restore to a dump image, and the selected files are extracted into the current directory. Table 10.9 shows some of the important restore command-line switches.

## TIP
> A piped combination of dump and restore can duplicate the contents of one filesystem onto another filesystem.

## TABLE 10.9
**Noteworthy restore Command-Line Options**

| OPTION | DESCRIPTION |
|---|---|
| `-C` | Compares the contents of the archive with the current filesystem and no restore takes place. You can use this option to check what has changed since your last backup. |
| `-f file` | Specifies the archive file. Like dump, it also defaults to `/dev/tape` and will check the TAPE environment variable if that fails. |
| `-h directory` | Extracts only the directory when specified, rather than its contents. |
| `-i` | Performs interactive restoration of specified files. This option also allows you to browse the dump image and flag files or directories to be extracted later. |
| `-r` | Allows you to rebuild the filesystem from the dump image. Use this option if you need to do bare-metal recovery from a tape. It expects a clean filesystem (that is, it expects you to have just run `mke2fs`). This operation is not interactive and should not be done unless you intend to actually restore the filesystem itself rather than just extract a couple of files. |
| `-R` | Resumes interrupted full restoration. |
| `-s fileno` | Specifies the position of the archive on the tape. This capability is useful when there are multiple dump images on the same media. |
| `-t file` | Lists filenames on the backup archive but does not restore them. |
| `-T` | Specifies the temporary directory. |
| `-v` | Produces verbose output. |
| `-x file`<br>`-X fileset` | Extracts only the named files from the archive. The uppercase `-X` instead reads a list of files to restore from a flat ASCII text file. |
| `-y` | Does not query on error. |

The restore utility is not too difficult to use but can be rather tricky when you’re dealing with multiple dump images on the same media. Therefore, you should be familiar with it before you really have to use it. The following are two sample restore commands:

- Retrieves all the files from the archive in tape media and writes them under the current directory:
  ```
  restore -rf /dev/st0
  ```
- Performs an interactive restoration from the third dump image on the tape media:
  ```
  restore -is 3 -f /dev/st0
  ```
