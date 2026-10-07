
# Table 11.5 tar Commands

| Command | Abbreviation | Purpose |
|---|---|---|
| --create | c | Creates an archive. |
| --concatenate | A | Appends tar files to an archive. |
| --append | r | Appends files to an archive. |
| --update | u | Appends files that are newer than those in an archive. |
| --diff or --compare | d | Compares an archive to files on disk. |
| --list | t | Lists archive contents. |
| --extract or --get | x | Extracts files from an archive. |

# Table 11.6 tar Qualifiers

| Qualifier | Abbreviation | Purpose |
|---|---|---|
| --directory dir | C | Changes to directory *dir* before performing operations. |
| --file [host:]file | f | Uses called *file* on computer called *host* as the archive file. |
| --listed-incremental file | g | Performs incremental backup or restore, using *file* as a list of previously archived files. |
| --one-file-system | l | Backs up or restores only one file-system (partition). |
| --multi-volume | M | Creates or extracts a multi-tape archive. |
| --tape-length N | L | Changes tapes after *N* kilobytes. |
| --same-permissions | p | Preserves all protection information. |

# Table 11.6 tar Qualifiers (continued)

| Qualifier | Abbreviation | Purpose |
|---|---|---|
| --absolute-paths | P | Retains the leading / filenames. |
| --verbose | V | Lists all files read or extracted. |
| --verify | W | Verifies the archive after writing it. |
| --exclude file | (none) | Excludes file from the archive. |
| --exclude-from file | X | Excludes files listed in file the archive. |
| --gzip or --ungzip | z | Processes the archive through gzip or gunzip. |

Of the commands listed in Table 11.5, the most commonly used are --create, --extract, and --list. The most useful qualifiers from Table 11.6 are --file, --listed-incremental, --one-file-system, --same-permissions, --gzip, and --verbose.

> **WARNING** The tar --one-file-system option is critically important to backups. Ordinarily, tar backs up everything under the directory it is given as input. Although this works if you feed tar the name of a directory that has nothing mounted on, it can cause problems for certain types of mounts. For example, if you tell tar to back up the root directory (which is, /), the program backs everything mounted on that directory or any subdirectory, including NFS or Samba shares served by other machines. Also, tar also backs up the Linux /proc filesystem, which is a virtual filesystem that represents the computer's status, including all its memory. At restoration time, it tries to overwrite the /proc filesystem's contents, which is likely to cause serious problems, possibly even including a system crash. For this reason, it's best to use --one-file-system and feed the name of each partition you want to back up.

The tar command backs up to or from files. Because Linux treats hardware devices as if they were files, you can tell tar to back up or to an appropriate hardware device file, in order to use that device directly. This approach works best for tape devices; for CD-R and CD-RW drives, it's necessary to pipe tar's output through CD-R software like drecord, and for disk devices, it's best to store the archive as a regular file on a filesystem, although you can store the archive "raw" to the device).

# A Sample tar Operation

A typical tar command to back up a computer looks like this:

```bash
# tar --create --verbose --gzip --one-file-system --same-permissions
  --file /dev/st0 / /home /usr/local
```

This command can be expressed somewhat succinctly using command abbreviations:

```bash
# tar cvzlpf /dev/st0 / /home /usr/local
```

In either format, this tar command backs up the root ( ), /home, and /usr/local filesystems to /dev/st0 (the first SCSI tape device). The assumption here is that the computer has three Linux partitions, corresponding to the three specified directories. A system with different partitions would need to specify the appropriate local partitions.

For an incremental or differential backup, you could add the --listed-incremental parameter, in this example:

This command stores information on the incremental backup in the /root/increments file, and uses the contents of that file to designate which files are to be backed up. To perform a series of incremental backups, you would issue the command as above. Before running another backup, you would make a copy of the increments file. After making backup, overwrite the new increments file with the backup. This way, tar will back up the same files the next time you use this option, plus any additional ones that changed. To perform a differential backup, you would leave the increments file alone and refer to it each time you do a backup. tar will then modify the increments file, and will back up only files changed since the last incremental backup.

If you want to create multiple archives on a single tape, you must use the mt command, described earlier in this chapter, in conjunction with a nonrewinding tape device. You can then step past existing archives to read or write second, third, and subsequent archives.

# Archiving to a Local Directory

You can use tar to create compact archives of files that you can then move around, on floppy disks or the like, or transfer over a network. The command

```bash
# tar cvzf archive.tgz /usr/local/bin
```

creates a compressed archive of the /usr/local/bin directory and names that archive archive.tgz. The archive is created in the directory from which the command was issued. The output looks something like this:

```
tar: Removing leading '/' from archive names
usr/local/bin/
usr/local/bin/gpg-check
usr/local/bin/gpg-encrypt
usr/local/bin/gpg-sign
usr/local/bin/gpg-sign+encrypt
```

The command tar xvzf archive.tgz uncompresses the archive and sends the output to a directory under the current directory; tar uses relative pathnames by default. If the usr/local/bin directory doesn't exist in the working directory, it will be created.

The command to read a listing of archive's contents with tar, following the same format, is tar -f archive.tgz. The output will include the file paths and the equivalent of an ls -1.

If you wish to use full paths—to write to /usr/local/bin without regard to the directory from which the command was run—you can use the P qualifier. The resulting commands would be

```bash
# tar cvzPf archive.tgz /usr/local/bin
```

and

```bash
# tar xvzPf archive.tgz
```

The output would list the full paths instead of the relative paths listed earlier and would be identical for the archive and extract commands:

```
/usr/local/bin/
/usr/local/bin/gpg-check
/usr/local/bin/gpg-encrypt
/usr/local/bin/gpg-sign
/usr/local/bin/gpg-sign+encrypt
```

Unpacking this archive with the command we used before would put the files into /usr/local/bin instead of /current/directory/usr/local/bin.

![](img/4fb617eb648f87def380ef5d92052d01_400_0)

# Chapter 11 Backing Up and Restoring

On occasion, you may want to move files from one location to another. You can use cp to do this, cp tends to drop ownership and other information. Rather than remember the cp parameters to work around these problems, you may want to use tar. You can use a Linux pipe to do this, tarring files to another location, thus:

```bash
# cp /source-dir
# tar cpf - | cd /destination-dir; tar xpf -
```

The result of the preceding two commands is a duplication of /source-dir in /destination-dir, including ownership, permissions, symbolic links. This command can be very useful if you want to back up to backup hard disk. If your system goes down, you can swap in the backup hard disk, boot with an emergency boot floppy, and by running the backup system in a matter of minutes.

# Archiving to Another Computer Remotely

To archive the file to another computer, you simply precede the archive name with the name of the computer followed by a colon. This option, like the remote dump access described earlier, uses rsh or ssh on the destination system, so you can access a remote tape drive directly. Thus the archival commands would be some like:

```bash
# tar cvzf remote:/dev/st0 /usr/local/bin
# tar xvzf remote:/dev/st0
```

# Archiving to a Floppy Disk

Yes, Virginia, it is possible to back up your system to floppy disks, but it will be painful. Each floppy disk will hold 1.4MB of data. This technique is most useful for copying large files from one system to another using floppies, or copying files between Linux and other Unix systems that don't share filesystems. By writing a tar directly to floppy, you bypass the need for a filesystem. Assume you have a file /tmp/biggraphic.gif, with a size of 1.88MB. Obviously this won't fit on a standard 3.5" floppy. You can use the tar command with the -M floppy.

```bash
# tar -cvMf /dev/fd0 /tmp/biggraphic.gif
```

When the backup image reaches the floppy's capacity, you will be prompted for a new floppy:

Prepare volume #2 for /dev/fd0 and hit return:

Put the second floppy in the drive and press the Enter key, and tar will continue the backup process. Each time the floppy capacity is exceeded, you will get this same prompt with an appropriate volume number.
