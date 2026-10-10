In the above-mentioned example, the `-0` option tells `dump` to perform a full backup. The `-A` option is used to designate the archive file, which is read by the `restore` command (described below) when restoring the backed up files. `-f` is used to identify the target file or device that will host the “dumped” files. The number of options for `dump` is astounding, and I recommend that you consult the `man` page if you need to perform specific types of backups.

# restore

The `restore` command performs the inverse function of `dump`. It restores files that have been backed up using `dump`. The `restore` command can be used to restore a full backup of a file system and apply any subsequent incremental backups, `restore` can also be used to restore individual files or directories from a full or partial backup file archive. Like its counterpart, `restore` can operate across a network to restore filesystems or files and directories on remote systems.

The following is the basic syntax for `restore` that will restore all files from the identified archive (mounted at /dev/nst0) in the current directory:

```
restore rf /dev/nst0
```

In this example, the `r` option retrieves all files from the archive and the `f` option is used to designate the archive (\dev/nst0). `restore` also has an interactive mode, accessed using the `-I` option, that lets you navigate inside the archive to select individual files and directories to restore. The syntax for that looks like this:

```
restore If /dev/nst0
```

Like `dump`, the number of options for `restore` is numerous. Its `man` page is worth consulting for performing specific file restore operations.

# dd

The `dd` command is a prime example of a big thing that comes in a small package. This seemingly simple tool is incredibly useful for making and copying disk images, backing up and moving disks, and duplicating filesystems. It makes an exact clone of a hard disk, including all blank space. To use it, the source disk must be unmounted and the output destination must be at least as large as the source.

To illustrate, the following syntax will create an image file in my home directory entitled, cddbackup.iso from the CD in my CD-ROM drive:

```
dd if=/dev/cdrom of=/home/brian/cddbackup.iso
```

The option, `if`, designates the input file (the CD that is mounted in my CD-ROM drive) and `of` designates the output file, cddbackup.iso in my home