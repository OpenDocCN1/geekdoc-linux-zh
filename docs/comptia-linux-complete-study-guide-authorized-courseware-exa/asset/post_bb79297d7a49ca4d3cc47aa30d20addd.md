
## The `which` Command (Continued)

search for all matches by adding the -a option.) For instance, you might want to know where the xterm program is located:

```
$ which xterm
/usr/bin/xterm
```

Because the files that `which` finds are on your path, it won't help you to run these programs. Instead, it's likely to be useful if you need to know the complete path for some reason—say, because you want to call the program from a script and don't want to make assumptions about the path available to the script and so want to include the complete path in the script.

## The `type` Command

This command isn't really a search command; instead, it tells you how a command you type will be interpreted—as a built-in command, an external command, an alias, and so on. For instance, you can use it to identify several common commands:

```
$ type type
type is a shell builtin
$ type cat
cat is /bin/cat
$ type ls
ls is aliased to 'ls --color'
```

This example identifies `type` itself as a built-in shell command, `cat` as a separate program stored in `/bin`, and `ls` as an alias for `ls --color`. You can add several options to modify the command's behavior. For instance, `-t` shortens the output to `builtin`, `file`, `alias`, or `other` short identifiers; and `-a` provides a complete list, for instance providing both the alias expansion and the location of the ultimate executable when provided with an alias name.

In Exercise 4.2, you'll get to use several ways to locate files.

## EXERCISE 4.2

### Locating Files

This exercise demonstrates several methods of locating files. You'll locate the `startx` program. (If your system doesn't have X installed, you can try searching for another program or file, such as `pwd` or `fstab`. You may need to change the path passed to `find` in step 5.) To find a file, follow these steps:

- 1. Log into the Linux system as a normal user.
- 2. Launch an xterm from the desktop environment's menu system if you used a GUI login method.
- 3. Type `locate startx.` The system should display several filenames that include the string `startx`. This search should take very little time. (A few distributions lack the `locate` command, so this step won't work on some systems.)
- 4. Type `whereis startx.` The system responds with the names of a few files that contain the string `startx`. Note that this list may be slightly different than the list returned by step 3 but that the search proceeds quickly.
- 5. Type `find /usr -name startx.` This search takes longer, and when run as an ordinary user, most likely returns several `Permission denied` error messages. It should also return a single line listing the `/usr/bin/startx` or `/usr/X11R6/bin/startx` program file. Note that this command searches only `/usr`. If you searched `/`, the command would take more time.
- 6. Type `which startx.` This search completes almost instantaneously, returning the complete filename of the first instance of `startx` the system finds on its path.
- 7. Type `type startx.` Again, the search completes very quickly. It should identify `startx` as an external command stored at `/usr/bin/startx`, `/usr/X11R6/bin/startx`, or possibly some other location.

## Summary

File management is basic to being able to administer or use a Linux system. Various commands are useful to both users and administrators for copying, moving, renaming, and otherwise manipulating files and directories. You may also want to set up access controls, both to limit the amount of disk space users may consume and to limit who may access specific files and directories. Finally, Linux provides tools to help you locate files using various criteria.

## Exam Essentials

**Describe commands used to copy, move, and rename files in Linux.** The `cp` command copies files, as in `cp first second` to create a copy of first called second. The `mv` command does double duty as a file-moving and a file-renaming command. It works much like `cp`, but `mv` moves or renames the file rather than copying it.

**Summarize Linux's directory-manipulation commands.** The `mkdir` command creates a new directory, and `rmdir` deletes a directory. You can also use many file-manipulation commands, such as `mv` and `rm` (with its `-r` option), on directories.

**Explain the difference between hard and symbolic links.** Hard links are duplicate directory entries that both point to the same inode and hence to the same file. Symbolic links are special files that point to another file or directory by name. Hard links must reside on a single filesystem, but symbolic links may point across filesystems.

**Summarize the common Linux archiving programs.** The `tar` and `cpio` programs are both file-based archiving tools that create archives of files using ordinary file access commands. The `dd` program is a file-copy program; but when it’s fed a partition device file, it copies the entire partition on a very low-level basis, which is useful for creating low-level image backups of Linux or non-Linux filesystems.

**Describe Linux’s file ownership system.** Every file has an owner and a group, identified by number. File permissions can be assigned independently to the file’s owner, the file’s group, and all other users.

**Explain Linux’s file permissions system.** Linux provides independent read, write, and execute permissions for the file’s owner, the file’s group, and all other users, resulting in nine main permission bits. Special permission bits are also available, enabling you to launch program files with modified account features or alter the rules Linux uses to control who may delete files.

**Summarize the commands Linux uses to modify permissions.** The `chmod` command is Linux’s main tool for setting permissions. You can specify permissions using either an octal (base 8) mode or a symbolic notation. The `chown` and `chgrp` commands enable you to change the file’s owner and group, respectively. (The `chown` command can do both but can only be run by root.)

**Describe the prerequisites of using Linux’s disk quota system.** Linux’s disk quota system requires support in the Linux kernel for the filesystem on which quotas are to be used. You must also run the `quotaon` command, typically from a SysV startup script, to enable this feature.

**Explain how quotas are set.** You can edit quotas for an individual user via the `edquota` command, as in `edquota larry` to edit Larry’s quotas. This command opens an editor on a text file that describes the user’s quotas. You can change this description, save the file, and exit from the editor to change the user’s quotas.

**Summarize how Linux’s standard directories are structured.** Linux’s directory tree begins with the root (/) directory, which holds mostly other directories. Specific directories may hold specific types of information, such as user files in `/home` and configuration files in `/etc`. Some of these directories and their subdirectories may be separate partitions, which helps isolate data in the event of filesystem corruption.

**Describe the major file-location commands in Linux.** The `find` command locates files by brute force, searching through the directory tree for files that match the criteria you specify. The `locate` (or `slocate`) command searches a database of files in important directories. The `whereis` command searches a handful of important directories, and `which` searches the path. The `type` command identifies another command as a built-in shell command, a shell alias, or an external command (including the path to that command).

## Review Questions

1. You want to use `/media/cdrom` to access your CD-ROM drive, so you insert a CD-ROM into the drive and type `mount /media/cdrom /dev/cdrom` as root. You receive the error message `/media/cdrom is not a block device.` Why did this happen?
   - A. You must first prepare the mount point by typing `mountpoint /media/cdrom`; only then will the `mount` command succeed.
   - B. The command reverses the order of the CD-ROM device file and the mount point; it should be `mount /dev/cdrom /media/cdrom`.
   - C. The `/dev/cdrom` filename isn’t valid; you must determine what device file is associated with your CD-ROM drive.
   - D. The CD-ROM is defective or the CD-ROM drive is malfunctioning. Try another CD-ROM and, if necessary, replace the drive.

2. What is wrong with the following `/etc/fstab` file entry? (Select all that apply.)
   `/dev/hda8  nfs  default  0 0`
   - A. The entry is missing a mount point specification.
   - B. All `/etc/fstab` fields should be separated by commas.
   - C. The `default` option may only be used with ext2 file systems.
   - D. `/dev/hda8` is a disk partition, but `nfs` indicates a network filesystem.

3. You want to discover the sizes of several dot files in a directory. Which of the following commands might you use to do this?
   - A. `ls -la`
   - B. `ls -p`
   - C. `ls -R`
   - D. `ls -d`

4. You want to move a file from your hard disk to a USB pen drive. Which of the following is true?
   - A. You’ll have to use the `--preserve` option to `mv` to keep ownership and permissions set correctly.
   - B. The `mv` command will adjust filesystem pointers without physically rewriting data if the pen drive uses the same filesystem type as the hard disk partition.
   - C. You must use the same filesystem type on both media to preserve ownership and permissions.
   - D. The `mv` command will delete the file on the hard disk after copying it to the pen drive.
