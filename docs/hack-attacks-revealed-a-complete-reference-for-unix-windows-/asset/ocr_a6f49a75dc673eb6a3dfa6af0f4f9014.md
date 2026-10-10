attrib [+−r] [+−a] [drive:]pathname [/s]

Where:

+   - **+r** sets the read-only attribute of a file.
+   - **−r** disables read-only mode.
+   - **+a** sets the archive attribute of a file.
+   - **−a** clears the archive attribute of a file.

# Comments

The attrib command sets read-only and/or archive attributes for files. You may use wildcards to specify a group of files. Attrib does not accept a directory name as a valid filename. The drive and pathname specify the location of the file or files. The /s switch processes all subdirectories as well as the path specified.

The backup, restore, and xcopy commands use the archive attribute as a control mechanism. You can use the +a and −a options to select files that you want to back up with the backup /m command, or copy with xcopy /m or xcopy /a.

# Example

To display the attribute of a file called *report* on the default drive, type the following:

```
attrib report
```

# Backup

This command backs up one or more files from one disk to another.

# Syntax

```
backup [drive1:][path]filename] [drive2:] [/s][/m][/a][/f] [/d:date] [/t:time] [/L:[[drive:][path]filename]]
```

Where drive1 is the disk drive that you want to back up, and drive2 is the target drive to which the files are saved.

# Comments

The backup command can back up files on disks of different media (hard disks and floppy). Backup also backs up files from one floppy disk to another, even if the disks have a different number of sides or sectors. Backup switches are:

+   - **/s** Backs up subdirectories.
+   - **/m** Backs up only those files that have changed since the last backup.
+   - **/a** Adds the files to be backed up to those already on a backup disk.