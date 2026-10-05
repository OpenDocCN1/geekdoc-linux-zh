# SuSE System Administration
PART III

mentioned, the find command can find files that are newer than a specified file. The touch command updates the time of a file; therefore, it is easy to touch a file after a backup has completed. Then, at the next backup, you simply search for files that are newer than the file you touched. The following example searches for files that are newer than the file /tmp/last_backup and performs a cpio to archive the data:

```
$ find -newer /tmp/last_backup -print | cpio > /dev/rmt0
```

With tar, the same action is completed in the following way:

```
$ find -newer /tmp/last_backup | tar cTF -> /dev/rmt0
```

> Note
nYou want to touch the file before you start the backup. This means you have to use different files for each level of backup, but it ensures that the next backup gets any files modified during the current backup.

# Performing Backups with the taper Command

The taper command (/sbin/taper), included with SuSE Linux, is a backup and restore program with a curses-interface you can use to maintain compressed or uncompressed archives on tapes or removable media (even over a network!). Using taper is easy; the format of a taper command line looks like the following: 

```
# taper <-T tape-type> <option> <device>
```

You first need to decide what type of device (or media) you'd like to use with taper. This program supports a number of devices, which are listed in Table 20.2 along with the command lines to:

TABLE 20.2 Device Support by taper
| Device | Type | Command Line |
| /dev/zftape | Floppy tape driver | # taper -T z |
| /dev/ht0 | IDE tape driver | # taper -Ti |
| file | File on hard disk | # taper -T1 |
| /dev/ftape | Floppy tape drive | # taper -Tf |
| /dev/fd0 | Removable floppy drive | # taper -Tr |
| /dev/sda4 | Removable Zip drive | # taper -Tr -b /dev/sda4 (-b notes the device and archive file) |
| /dev/sda | SCSI tape drive | # taper -Ts |