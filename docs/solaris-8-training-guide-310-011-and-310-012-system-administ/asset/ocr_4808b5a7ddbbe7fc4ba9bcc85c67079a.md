Be aware that even with the backup schedule outlined in Table 11.9, data can still be lost. If a hard disk fails at 3 p.m., all modifications since the 4:30 a.m. backup will be lost. Also, files that were deleted midweek will not appear on the level 5 tapes. Sometimes, a user accidentally deletes a file and does not realize it for several weeks. When the user wants to use the file, it is not there. If he asks you to restore it from backup, the only tape it appears on is the level 0, and it could be too far out of date to be useful. By not overwriting the daily level 9 tapes frequently, you can minimize this problem.

The syntax for the ufsdump command is as follows:

```
/usr/sbin/ufsdump <options> <arguments> <files to dump>
```

The options to the ufsdump command are described in Table 11.10.

# TABLE 11.10

# ufsdump Options

| Option | Description |
|---|---|
| <options> | A single string of one-letter option names. |
| <arguments> | Option arguments that can be multiple strings. The option letters and the arguments that go with them must be in the same order. |
| <files to dump> | The files to back up. This argument must always come last. It specifies the source or contents of the backup. It usually identifies a file system, but it can also identify individual files or directories. For a file system, specify the name of the file system or the raw device file for the disk slice where the file system is located. |

Table 11.11 describes the options and arguments for the ufsdump command.

# TABLE 11.11

# OPTIONS FOR THE ufsdump COMMAND

| Option | Description |
|---|---|
| 0 to 9 | Backup level. Specify level 0 for a full backup of the entire file system. Levels 1–9 are for incremental backups of files that have changed since the last lower-level backup. |