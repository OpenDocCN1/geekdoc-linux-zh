
# BACKING UP FILES 601

Many options, you have a few in many situations. The following command plays a complete list of options:

```bash
$ tar --help | less
```

Most options for tar can be given either in a short form (a single letter) or as a descriptive word. Descriptive-word options are preceded by hyphens, as --help. Single-letter options can be combined into a single command-line argument and not be preceded by a hyphen (for consistency with other utilities, it is good practice to use the hyphen anyway).

Although the following two commands look quite different, they specify the same tar options in the same order. The first version combines single-letter options into a single command-line argument; the second version uses descriptive words for the options:

```bash
$ tar -ztvf /dev/st0 --list --verbose --file /dev/st0
```

Both commands tell tar to generate a (v, verbose) table of contents (t, list) from the tape on /dev/st0 (f, file), using gzip (z, gzip) to compress the files. Unlike the original UNIX tar, the GNU version strips the leading / from absolute pathnames.

The options in Table 16-1 tell the tar program what to do. You must include exactly one of these options in a tar command.

The -c, -t, and -x options are used most frequently. You can use many other options to change how tar operates. The -j option, for example, compresses and decompresses the file by filtering it through bzip2 (page 174).

## Table 16-1 tar options

| Option | Effect |
| :--- | :--- |
| --append (-r) | Appends files to an archive |
| --concatenate (-A) | Adds one or more archives to the end of an existing archive |
| --create (-c) | Creates a new archive |
| --delete | Deletes files in an archive (not on tapes) |
| --dereference (-h) | Follows symbolic links |
| --diff (-d) | Compares files in an archive with disk files |
| --extract (-x) | Extracts files from an archive |
| --help | Displays a help list of tar options |
| --list (-t) | Lists the files in an archive |
| --update (-u) | Like the -r option, but the file is not appended if a newer version is already in the archive |

## cpio: ARCHIVES FILES

cpio (copy in/out) program is similar to tar but can read and write archive files in various formats, including the one used by tar. Normally cpio reads the names of the files to add to the archive from standard input and produces the archive file as standard output. When extracting files from an archive, it reads the archive as standard.

As with tar, some options can be given in both short, single-letter format and a more descriptive word form. However, unlike tar, the syntax of the two forms in cpio differs when the option must be followed by additional information. In the short form, you must include a SPACE between the option and the additional information; with the word form, you must separate the two with an equal sign and no SPACE.

Running cpio with the --help option displays a complete list of options.

## PERFORMING A SIMPLE BACKUP

When you prepare to make a major change to a system, such as replacing a disk drive, upgrading to a new release, or updating the Linux kernel, it is a good idea to archive all of the files so you can restore any become damaged if something goes wrong. For this type of backup, tar or cpio works well. For example, if you have a SCSI tape drive as /dev/st0 (or it could be a /dev/hdb) that is capable of holding all the files on a single tape, you can use the following commands to construct a backup tape of the entire system:

```bash
$ cd /
$ sudo tar -cf /dev/st0
```

All the commands in this section start by using cd to change to the root directory you are sure to back up the entire system. The tar command then creates an archive (c) on the device /dev/st0 (f). To compress the archive, replace the preceding command with the following command, which uses j to call bzip2:

```bash
$ sudo tar -cjf /dev/st0
```

You can back up a system with a combination of find and cpio. The following commands create an output file and set the I/O block size to 5120 bytes (the default is 512):

```bash
$ cd /
$ sudo find -depth | cpio -oB > /dev/st0
```

The next command restores the files in the /home directory from the preceding backup. The option extracts files from an archive (-i) in verbose mode, keeping the modification times and creating directories as needed.

```bash
$ cd /
$ sudo cpio -ivmd /home/* < /dev/st0
```

Although all the archive programs work well for simple backups, utilities such as amanda (page 600) provide more sophisticated backup and restore systems. For example, to determine whether a file is in an archive, you must read the entire archive. If the archive is split across several tapes, this process is particularly tiresome. More sophisticated utilities, including amanda, assist you in several ways, keeping a table of contents of the files in a backup.

## Exclude directories from a backup

Tip in practice, you will likely want to exclude some directories from the backup process. For example, not backing up /tmp or /var/tmp can save room in the archive. Also, do not back up directories that are not needed for restoration.

### Exclude directories from a backup (Note: OCR text appears repetitive/corrupted in this section, maintaining logical flow)

(Note: The source OCR text for pages 653-654 contains significant repetition and garbled phrases. I have cleaned the legible parts while preserving the technical context provided.)
