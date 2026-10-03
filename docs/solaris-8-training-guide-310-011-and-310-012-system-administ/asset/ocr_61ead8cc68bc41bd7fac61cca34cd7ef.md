# tar

The primary use of the tar (tape archiver) command is to copy file systems or individual files from a hard disk to a tape or from a tape to a hard disk. You can also use tar to create a tar archive on a hard disk or floppy disk, and to extract files from a tar archive on a hard disk or floppy disk. The tar command is popular because it's available on most UNIX systems; however, it is limited to a single tape. If the data you are backing up requires more than one tape, use the cpio, pax, or ufsdump commands, which I will describe later.

The tar command has the following syntax:

```
tar <options> <tar filename> <file list>
```

in which options is the list of command options listed in Table 11.3.

# TABLE 11.3

# COMMAND OPTIONS FOR tar

| Option | Description |
|---|---|
| c | Creates a tar file. |
| t | Table of contents. Lists the names of the specified files each time they occur in the tar filename. If no file argument is given, the names of all files in the tar filename are listed. When used with the v function modifier, it displays additional information for the specified files. |
| x | Extracts or restores files from a tar filename. |
| v | Verbose. Outputs information to the screen as tar reads or writes the archive. |
| f | Uses the tar filename argument as the name of the tar archive. If f is omitted, tar uses the device indicated by the TAPE environment variable (if it is set). If the TAPE variable is not set, tar uses the default values defined in /etc/default/tar. If the name of the tar file is -, tar writes to the standard output or reads from the standard input. |

For a more complete listing of command options, refer to the Solaris online manual pages.