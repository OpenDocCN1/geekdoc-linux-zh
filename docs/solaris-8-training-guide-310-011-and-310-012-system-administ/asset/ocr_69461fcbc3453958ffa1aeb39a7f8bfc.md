+   - The root_device keyword if the systems being upgraded by the class file have more than one root file system that can be upgraded

A class file allows the following:

+   - A comment after the pound sign (#) anywhere on a line. If a line begins with a #, the entire line is a comment. If a # is specified in the middle of a line, everything after the # is considered a comment.
- Blank lines

The class file is made up of keywords and their values. They are described in the following sections.

# backup_media

backup_media defines the medium that is used to back up file systems if they need to be reallocated during an upgrade because of space problems. If multiple tapes or disks are required for the backup, you are prompted to insert these during the upgrade. Here is the backup_media syntax:

```
backup_media <type> <path>
```

type can be one of the keywords listed in Table 21.5.

TABLE 21.5
BACKUP_MEDIA KEYWORDS

| Keyword | Description |
|---|---|
| local_tape | Specifies a local tape drive on the system being upgraded. The <path> must be the character (raw) device path for the tape drive, such as /dev/rmt/0. |
| local_diskette | Specifies a local diskette drive on the system being upgraded. The <path> is the local diskette, such as /dev/rdiskette0. The diskette must be formatted. |
| local_filesystem | Specifies a local file system on the system being upgraded. The <path> can be a block device path for a disk slice or the absolute <path> to a file system mounted by the /etc/vfstab file. Examples of <path> are /dev/dsk/c0t0d0s7 and /home. |