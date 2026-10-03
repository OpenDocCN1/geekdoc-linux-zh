| Option | Description |
|---|---|
| s | Estimates the size of the backup. Determines the amount of space needed to perform the backup (without actually doing it) and outputs a single number indicating the estimated size of the backup in bytes. |
| t <tracks> | Tracks. Specifies the number of tracks for 1/4-inch cartridge tape. You need to use this option only when ufsdump cannot detect the end of the medium. |
| u | Updates the dump record. For a completed backup of a file system, adds an entry to the file /etc/dumpdates. The entry indicates the device name for the file system's disk slice, the backup level (0 to 9), and the date. No record is written when you do not use the u option or when you back up individual files or directories. If a record already exists for a backup at the same level, it is replaced. |
| v | Verify. After each tape or disk is written, verifies the contents of the medium against the source file system. If any discrepancies occur, prompts the operator to mount a new medium and then repeats the process. Use this option on an unmounted file system only; any activity in the file system causes it to report discrepancies. |
| w | Warning. Lists the file systems appearing in /etc/dumpdates that have not been backed up within a day. When you use this option, all other options are ignored. |
| w | Warning with highlight. Shows all file systems that appear in /etc/dumpdates, and highlights file systems that have not been backed up within a day. When you use this option, all other options are ignored. |

The ufsdump command uses these options by default:

```
ufsdump 9uf /dev/rmt/0 <files-to-back-up>
```

# ufsdump Examples

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
```