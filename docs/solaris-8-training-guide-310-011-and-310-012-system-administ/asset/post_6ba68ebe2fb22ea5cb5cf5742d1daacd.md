
Be aware that even with the backup schedule outlined in Table 11.9, data can still be lost. If a hard disk fails at 3 p.m., all modifications since the 4:30 a.m. backup will be lost. Also, files that were deleted midweek will not appear on the level 5 tapes. Sometimes, a user accidentally deletes a file and does not realize it for several weeks. When the user wants to use the file, it is not there. If he asks you to restore it from backup, the only tape it appears on is the level 0, and it could be too far out of date to be useful. By not overwriting the daily level 9 tapes frequently, you can minimize this problem.

The syntax for the ufsdump command is as follows:

/usr/sbin/ufsdump <options> <arguments> <files to dump>

The options to the ufsdump command are described in Table 11.10.

## TABLE 11.10
### ufsdump Options
| Option | Description |
|---|---|
| <options> | A single string of one-letter option names. |
| <arguments> | Option arguments that can be multiple strings. The option letters and the arguments that go with them must be in the same order. |
| <files to dump> | The files to back up. This argument must always come last. It specifies the source or contents of the backup. It usually identifies a file system, but it can also identify individual files or directories. For a file system, specify the name of the file system or the raw device file for the disk slice where the file system is located. |

Table 11.11 describes the options and arguments for the ufsdump command.

## TABLE 11.11
### OPTIONS FOR THE ufsdump COMMAND
| Option | Description |
|---|---|
| 0 to 9 | Backup level. Specify level 0 for a full backup of the entire file system. Levels 1–9 are for incremental backups of files that have changed since the last lower-level backup. |
| a `<archive-file>` | Instructs ufsdump to create an archive file. Stores a backup table of the tape contents in a specified file on the disk. The file can be understood only by ufsrestore, which uses the table to determine whether a file to be restored is present in a backup file and, if so, on which volume of the medium it resides. |
| b `<factor>` | Blocking factor. Specifies the number of 512-byte blocks to write to tape per operation. |
| c | Instructs ufsdump to back up to cartridge tape. When end-of-media detection applies, this option sets the block size to 126. |
| d `<bpi>` | Tape density. Use this option only when ufsdump cannot detect the end of the medium. |
| D | Diskette. Backs up to floppy disk. |
| f `<dump-file>` | Dump file. Specifies the destination of the backup. The dump-file argument can be one of the following:
- A local tape drive or disk drive
- A remote tape drive or disk drive
- Standard output
Use this argument when the destination is not the default local tape drive /dev/rmt/0. If you use the f option, you must specify a value for dump-file. |
| l | Autoload. Use this option if you have an autoloading (stack-loader) tape drive. When the end of a tape is reached, this option takes the drive offline and waits up to two minutes for the tape drive to be ready again. If the drive is ready within two minutes, it continues. If the drive is not ready after two minutes, autoload prompts the operator to load another tape. |
| n | Notify. When intervention is needed, this option sends a message to all terminals of all users in the sys group. |
| o | Offline. When ufsdump is finished with a tape or disk, it takes the drive offline, rewinds it (if it's a tape), and removes the medium if possible (for example, it ejects a disk or removes an 8mm autoloaded tape). |
| s `<size>` | Size. Specifies the length of tape in feet or the size of disk in a number of 1024-byte blocks. You need to use this option only when ufsdump cannot detect the end of the medium. |
| s | Estimates the size of the backup. Determines the amount of space needed to perform the backup (without actually doing it) and outputs a single number indicating the estimated size of the backup in bytes. |
| t <tracks> | Tracks. Specifies the number of tracks for 1/4-inch cartridge tape. You need to use this option only when ufsdump cannot detect the end of the medium. |
| u | Updates the dump record. For a completed backup of a file system, adds an entry to the file /etc/dumpdates. The entry indicates the device name for the file system's disk slice, the backup level (0 to 9), and the date. No record is written when you do not use the u option or when you back up individual files or directories. If a record already exists for a backup at the same level, it is replaced. |
| v | Verify. After each tape or disk is written, verifies the contents of the medium against the source file system. If any discrepancies occur, prompts the operator to mount a new medium and then repeats the process. Use this option on an unmounted file system only; any activity in the file system causes it to report discrepancies. |
| w | Warning. Lists the file systems appearing in /etc/dumpdates that have not been backed up within a day. When you use this option, all other options are ignored. |
| W | Warning with highlight. Shows all file systems that appear in /etc/dumpdates, and highlights file systems that have not been backed up within a day. When you use this option, all other options are ignored. |

The ufsdump command uses these options by default:

```
ufsdump 9uf /dev/rmt/0 <files-to-back-up>
```

## ufsdump Examples

The following examples illustrate the use of the ufsdump command.

The following is an example of a full backup of the /users file system:

```
ufsdump 0ucf /dev/rmt/0 /users
DUMP: Writing 63 Kilobyte records
DUMP: Date of this level 0 dump: Sat Dec 12 13:13:22 1998
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/rdsk/c0t1d0s0 (pyramid1:/users) to /dev/rmt/0.
DUMP: Mapping (Pass I) [regular files]
DUMP: Mapping (Pass II) [directories]
DUMP: Estimated 10168 blocks (4.96MB).
DUMP: Dumping (Pass III) [directories]
DUMP: Dumping (Pass IV) [regular files]
DUMP: Tape rewinding
DUMP: 10078 blocks (4.92MB) on 1 volume at 107 KB/sec
DUMP: DUMP IS DONE
```

In the following example, the local /export/home file system on a Solaris 8 system is backed up to a tape device on a remote Solaris 8 system called sparc1:

```
ufsdump 0ucf sparc1:/dev/rmt/0 /export/home
DUMP: Date of this level 0 dump: Sat Dec 12 11:50:13 1998
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/rdsk/c0t3d0s7 (/export/home) to \
/dev/rmt/0 on host sparc1
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 19574 blocks (9.56MB)
DUMP: Writing 63 Kilobyte records
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: level 0 dump on Tue Oct 25 10:30:53 1994
DUMP: Tape rewinding
DUMP: 19574 blocks (9.56MB) on 1 volume
DUMP: DUMP IS DONE
```

If you want to see how much space a backup is going to require, issue the following command:

```
ufsdump 0s <filesystem>
```

The estimated number of bytes needed on tape to perform the level 0 backup is displayed.

## ufsrestore

The ufsrestore command copies files from backups created using the ufsdump command. You can use ufsrestore to reload an entire file system from a level 0 dump and incremental dumps that follow it, or to restore one or more single files from any dump tape. If ufsrestore is run by root, files are restored with their original owner, last modification time, and mode (permissions).

The syntax for the ufsrestore command is as follows:

```
ufsrestore <options> <arguments> <filename(s)>
```

The options for the ufsrestore command are described in Table 11.12.

## TABLE 11.12
### ufsrestore Options
| Option | Description |
|---|---|
| <options> | Gives you the choice of one and only one of these options: i, r, R, t, or x. |
| <arguments> | Follows the options string with the arguments that match the options. |
| <filename(s)> | Specifies files to be restored as arguments to the x or t options, and must always come last. |

Table 11.13 describes some of the more common options and arguments for the ufsrestore command.

## TABLE 11.13
### COMMAND OPTIONS FOR ufsrestore
| Option | Description |
|---|---|
| i | Interactive. Runs ufsrestore in interactive mode. In this mode, you can use a limited set of shell commands to browse the contents of the medium and select individual files or directories to restore. See Table 11.14 for a list of available commands. |
| r | Recursive. Restores the entire contents of the medium into the current working directory, which should be the top level of the file system. Information used to restore incremental dumps on top of the full dump is also included. To completely restore a file system, use this option to restore the full (level 0) dump and then each incremental dump. This is intended for a new file system that was just created with the newfs command. |
| x <filename(s)> | Extract. Selectively restores the files you specify using the filename(s) argument. filename(s) can be a list of files and directories. All files under a specified directory are restored unless you also use the h option. If you omit filename(s) or enter . for the root directory, all files on all volumes of the medium (or from standard input) are restored. Existing files are overwritten, and warnings are displayed. |

continues
