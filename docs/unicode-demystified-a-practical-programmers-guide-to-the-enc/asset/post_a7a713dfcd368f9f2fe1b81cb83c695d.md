
# Modifiers

You can specify one or more modifiers following an option. If you use the -character form of the modifier, a leading hyphen is not required. However, it is good practice to use the hyphen unless you combine the modifier with other single-character modifiers.

If a modifier takes an argument, that must be the last one in a group. For example, the arguments are arranged legally in the following tar command:

```
$ tar -cb 10 -f /dev/ftape
```

On the other hand, the following tar command generates an error:

```
$ tar -cbf 10 /dev/ftape
t: Invalid value for blocksize
```

The error is generated because the -b modifier takes an argument but is not the last modifier in in a group. This is different from the original version of tar, used with many UNIX systems, that allowed this construct.

- --absolute-paths -P The default behavior of tar is to force all pathnames to be relative paths by stripping leading slashes. This option disables this feature, so any absolute pathnames remain as absolute.

- --block-compress Normally compresses (gzip) or decompresses (gzip) the entire archive at once. This technique does not work with archives that are on tape devices. This option, when used with one of the preceding compression or decompression options, allows tar to compress the archive on a block-by-block basis, which works well with tape archive.

- --block-size [n] -b Uses n as the blocking factor for creating an archive. When tar is creating an archive directly to a tape (When tar reads a tape archive, automatically determines the blocking factor). The value of n is the number of 512-byte blocks to write as a single block on the tape. When you do not specify n, it defaults to 20.

- --bzip -j Uses bzip2 (page 74) when creating the archive and extracting files from the ar-archive.

- --checkpoint Displays the names of directories it extracts from an archive.

- --compress or -Z Uses compress when creating the archive and uncompress when extracting files --uncompress from the archive.

- --dereference -h Follows symbolic links and includes the linked-to-files as if they were normal files and directories.

- --directory -C Changes the working directory to directory before processing.

- --exclude filename Does not process the file given as filename. If filename is a directory, no files or directories within that directory are processed.

- --exclude-filename Similar to the --exclude option except that filename identifies a file that contains a list of files to exclude from processing. Each file listed in filename must be on a separate line.

- --filename -f Uses filename as the name of the file (device) to hold the archive. The filename can be the name of an ordinary file, a device (such as a tape drive), or a device on another computer on your network. To give the name of a device on another computer, use the domain name of the other computer and a colon (:) in the device name. If your username on the other machine is different from the one you are using, you can precede the domain name with the username on the remote machine, followed by an @. The following command, given by Alex on kudos, causes tar to use tape device /dev/st0 on bravo to hold the archive, using the account for Scott on bravo to access the tape device:

```
$ tar -cf scott@bravo:/dev/st0
```

For the preceding command to work, the remote machine must be running the rsh daemon (see footnote 15 on page 373), Alex (working from kudos) must have permission to use Scott's account on bravo with rsh, Scott must be able to execute the rm unit on bravo (rm on the remote machine accepts the tape output and writes it to tape), and Scott must have write permission to /dev/st0 on bravo.

You can use a hyphen (-) in place of a filename as a way to refer to standard input when creating an archive and standard output when extracting from an archive. The two commands are equivalent ways of creating an archive of the files under the /home directory on /dev/st0:

```
$ tar -zcf /dev/st0 /home
$ tar -cf /home | gzip > /dev/st0
```

- --gzip -z Causes tar to use gzip to compress the archive while it is being created and decompress the archive when extracting from it. When reading from an archive, this option also causes tar to detect when an archive has been compressed with the compression utility. If compress was used, tar uses uncompress instead of gzip as the files are extracted.

- --ignore-tailed-read When creating an archive, tar normally quits with a nonzero exit status if any of the files in file-list is unreachable. This option allows tar to continue processing, skipping unreachable files.

- --interactive -w Asks you for confirmation before reading or writing each file. Respond with y if you want tar to take the action. Any other response causes tar not to take the action.

- 9. A more secure way of accomplishing the task is to do sending the output of tar to ssh, which runs a command on the remote machine that writes tar's output to the remote tape.

# 1346 tar

- --modification-time -m Sets the modification time to the time of extraction. Without this option tar attempts to maintain the modification time of the original file.

- --one-file-system -I When a directory name appears in file-list while reading files for an archive, tar recursively processes the files and directories below the named directory. With this option tar stays the filesystem the named directory is in does not read files and directories that exist on other filesystems.

- --sparse -S GNU/Linux allows you to have sparse files on disk. These are large, mostly empty files. The empty sections of sparse files do not take up any disk space. When tar copies one of these sparse files out of an archive, it normally expands to its full size. When you restore a sparse file from a tar backup, the file takes up its full space and may no longer fit in the same disk space as the original. option causes tar to handle sparse files efficiently so that they do not take unused space in the archive or when they are extracted.

- --tape-length n -L As for a new tape after writing n*1,024 bytes to the current tape. This feature is useful when building archives that are too big to fit on a single tape. When combined with the -t option, -v causes tar to display a more detailed list of the files, showing ownership, size, and other useful information for files in the archive.

# Notes

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

The GNU/Linux version of tar was developed by the GNU project and includes a large number of options and modifiers. Only the most commonly used options and modifiers are presented here. The --help displays all options and modifiers.

# Examples

The following example makes a copy of the /home/alex directory and all files and subdirectories within that directory onto a tape. The v modifier displays the list of files it writes to tape. This command erases anything that was already the tape. The message tar explains that the default action is to store all pathnames as relative instead of absolute, allowing you to extract the files into a different place on your disks:

```
$ tar -cvf /dev/ftape /home/alex
tar: Removing / from absolute names in the archive.
home/alex/
home/alex/.zhenv
```

In the next example, the same directory is saved on the tape device /dev/st0 with a blocking factor of 100. Without the v modifier, tar does not display the list of files it is writing to the tape. The command runs in the background and displays any messages after a new prompt:

```
$ tar -cb 100 -f /dev/st0 /home/alex &
[1] 4298
tar: Removing / from absolute names in the archive.
```

The next command displays the table of contents of the archive on tape device /dev/ftape:

```
$ tar -tvf /dev/ftape
drwxrxr-x alex/group Jun 30 21:39 2004 home/alex/
-rw-r-- alex/group 678 Aug 6 14:06 2003 home/alex/.zhenv
-rw-r-- alex/group 571 Aug 6 14:12 2003 home/alex/mail/
drw------ alex/group 0 Nov 6 22:34 2003 home/alex/mail/
-rw------ alex/group 2799 Nov 6 22:34 2003 home/alex/mail/sent-mail
```
