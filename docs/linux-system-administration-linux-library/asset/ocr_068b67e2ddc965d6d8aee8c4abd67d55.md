# Chapter 11 Backing Up and Restoring

> **NOTE** Because dump operates on a lower level of filesystem access than most other backup utilities, any dump program must have explicit support for any filesystem you use. The standard Linux dump utility handles ext2 filesystems, but not FAT filesystems or the experimental journaling filesystems described in Chapter 10. Trying to use dump on such filesystems won't cause problems, neither will it work. Linux's dump may eventually be upgraded to handle more filesystems, though.

# Basic dump Operation

The dump command's basic syntax is this:

```
dump [-level] [-b blocksize] [-B records] [-f file] [-u] directory
```

The meanings of these parameters are as follows:

+   - **level** The incremental level.
- **blocksize** The size (in bytes) of a dump block. Combined, blocksize and **records** The size of the tape in dump blocks allow dump to handle tapes that are smaller than the data to be backed; if dump must back more than blocksize records it pauses when it reaches this limit and prompts you to change tapes.
- **file** The file to which the backup should be written—normally a tape device file, as described earlier.
- **u** This parameter causes dump to store data about its backup history in /etc/dumpdays. Without this parameter, incremental backups won't work correctly.
- **directory** The directory or filesystem device file to be backed up.

The incremental dump backs up a file if it has changed since the previously recorded backup. A standard incremental scheme begins at level 0 and extends to level 9, 0 being a full dump and 1–9 being incremental. Each incremental level backs up all files changed since the last backup of a lower incremental level. If you perform a series of dump operations (say, one per day) using the non-0 dump level, the result is a series of incremental backups, as described earlier in this chapter. If you increase the dump level with each backup (say, 1 on Monday, 2 on Tuesday, and so on), the result is a series of differential backups,

# dump in Action

Suppose you want to implement an incremental backup strategy in which you would backup on Sundays and back up all files changed since Sunday every other day of the