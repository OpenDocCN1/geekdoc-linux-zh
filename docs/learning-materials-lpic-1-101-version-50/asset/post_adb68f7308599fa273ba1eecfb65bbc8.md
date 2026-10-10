
According to the standard, the basic directory structure is as follows:

## /
This is the root directory, the topmost directory in the hierarchy. Every other directory is located inside it. A filesystem is often compared to a “tree”, so this would be the “trunk” to which all branches are connected.

## /bin
Essential binaries, available to all users.

## /boot
Files needed by the boot process, including the Initial RAM Disk (initrd) and the Linux kernel itself.

## /dev
Device files. These can be either physical devices connected to the system (for example, /dev/sda would be the first SCSI or SATA disk) or virtual devices provided by the kernel.

## /etc
Host-specific configuration files. Programs may create subdirectories under /etc to store multiple configuration files if needed.

## /home
Each user in the system has a “home” directory to store personal files and preferences, and most of them are located under /home. Usually, the home directory is the same as the username, so the user John would have his directory under /home/john. The exceptions are the superuser (root), which has a separate directory (/root) and some system users.

## /lib
Shared libraries needed to boot the operating system and to run the binaries under /bin and /sbin.

## /media
User-mountable removable media, like flash drives, CD and DVD-ROM readers, floppy disks, memory cards and external disks are mounted under here.

## /mnt
Mount point for temporarily mounted filesystems.

## /opt
Application software packages.

## /root
Home directory for the superuser (root).

## /run
Run-time variable data.

## /sbin
System binaries.

## /srv
Data served by the system. For example, the pages served by a web server could be stored under */srv/www*.

## /tmp
Temporary files.

## /usr
Read-only user data, including data needed by some secondary utilities and applications.

## /proc
Virtual filesystem containing data related to running processes.

## /var
Variable data written during system operation, including print queue, log data, mailboxes, temporary files, browser cache, etc.

Keep in mind that some of those directories, like */etc*, */usr* and */var*, contain a whole hierarchy of subdirectories under them.

# Temporary Files

Temporary files are files used by programs to store data that are only needed for a short time. This can be the data of running processes, crash logs, scratch files from an autosave, intermediary files used during a file conversion, cache files and such.

## Location of Temporary Files

Version 3.0 of the *Filesystem Hierarchy Standard* (FHS) defines standard locations for temporary files on Linux systems. Each location has a different purpose and behavior, and it is recommended that developers follow the conventions set by the FHS when writing temporary data to disk.

### /tmp

According to the FHS, programs should not assume that files written here will be preserved between invocations of a program. The recommendation is that this directory be cleared (all files erased) during system boot-up, although this is not mandatory.

### /var/tmp

Another location for temporary files, but this one *should not be cleared* during the system boot-up. Files stored here will usually persist between reboots.

### /run

This directory contains run-time variable data used by running processes, such as process identifier files (.pid). Programs that need more than one run-time file may create subdirectories here. This location *must be cleared* during system boot-up. The purpose of this directory was once served by `/var/run`, and on some systems `/var/run` may be a symbolic link to `/run`.

Note that there is nothing which prevents a program from creating temporary files elsewhere on the system, but it is good practice to respect the conventions set by the FHS.

# Finding Files

To search for files on a Linux system, you can use the `find` command. This is a very powerful tool, full of parameters that can suit its behaviour and modify output exactly to your needs.

To start, `find` needs two arguments: a starting point and what to look for. For example, to search for all files in the current directory (and subdirectories) whose name ends in `.jpg` you can use:

```
$ find . -name '*.jpg'
./pixel_3a_seethrough_1.jpg
./Mate3.jpg
./Expert.jpg
./Pentaro.jpg
./Mate1.jpg
./Mate2.jpg
./Sala.jpg
./Hotbit.jpg
```

This will match any file whose last four characters of the name are .jpg, no matter what comes before it, as * is a wildcard for "anything". However, see what happens if another * is added at the end of the pattern:

```
$ find . -name '*.jpg*'
./pixel_3a_seethrough_1.jpg
./Pentaro.jpg.zip
./Mate3.jpg
./Expert.jpg
./Pentaro.jpg
./Mate1.jpg
./Mate2.jpg
./Sala.jpg
./Hotbit.jpg
```

The file Pentaro.jpg.zip (highlighted above) was not included in the previous listing, because even if it contains .jpg on its name, it did not match the pattern as there where extra characters after it. The new pattern means “anything .jpg anything”, so it matches.

> **TIP** Keep in mind that the -name parameter is case sensitive. If you wish to do a case-insensitive search, use -iname.

The *.jpg expression must be placed inside single quotes, to avoid the shell from interpreting the pattern itself. Try without the quotes and see what happens.

By default, find will begin at the starting point and descend through any subdirectories (and subdirectories of those subdirectories) found. You can restrict this behaviour with the -maxdepth N parameters, where N is the maximum number of levels.

To search only the current directory, you would use -maxdepth 1. Suppose you have the following directory structure:

```
directory
├─ clients.txt
├─ partners.txt -> clients.txt
└─ somedir
   ├─ anotherdir
   └─ clients.txt
```

To search inside somedir, you would need to use -maxdepth 2 (the current directory +1 level down). To search inside anotherdir, -maxdepth 3 would be needed (the current directory +2 levels down).

The parameter -mindepth N works in the opposite way searching only in directories at least N levels down.

The -mount parameter can be used to avoid find going down inside mounted filesystems. You can also restrict the search to specific filesystem types using the -fstype parameter. So `find /mnt -fstype exfat -iname "*report*"` would only search inside exFAT filesystems mounted under /mnt.

## Searching for Attributes

You can use the parameters below to search for files with specific attributes, like ones that are writable by your user, have a specific set of permissions or are of a certain size:

- **-user USERNAME**
  Matches files owned by the user USERNAME.
- **-group GROUPNAME**
  Matches files owned by the group GROUPNAME.
- **-readable**
  Matches files that are readable by the current user.
- **-writable**
  Matches files that are writable by the current user.
- **-executable**
  Matches files that are executable by the current user. In the case of directories, this will match any directory that the user can enter (x permission).
- **-perm NNNN**
  This will match any files that have exactly the NNNN permission. For example, -perm 0664 will match any files which the user and group can read and write to and which others can read (or rw-rw-r--).

You can add a - before NNNN to check for files that have at least the permission specified. For example, -perm -644 would match files that have at least 644 (rw-r--r--) permissions. This includes a file with 664 (rw-rw-r--) or even 775 (rwxrwx-r-x).

- **-empty**
  Will match empty files and directories.

- **-size N**
  Will match any files of N size, where N by default is a number of 512-byte blocks. You can add suffixes to N for other units: Nc will count the size in bytes, Nk in kibibytes (KiB, multiples of 1024 bytes), NM in mebibytes (MiB, multiples of 1024 * 1024) and NG for gibibytes (GiB, multiples of 1024 * 1024 * 1024).

Again, you can add the + or - prefixes (here meaning *bigger than* and *smaller than*) to search for relative sizes. For example, `-size -10M` will match any file less than 10 MiB in size.

For example, to search for files under your home directory which contain the case insensitive pattern report in any part of the name, have `0644` permissions, have been accessed 10 days ago and which size is at least 1 MiB, you could use

```
$ find ~ -iname "*report*" -perm 0644 -atime 10 -size +1M
```

# Searching by Time

Besides searching for attributes you can also perform searches by time, finding files that were accessed, had their attributes changed or were modified during a specific period of time. The parameters are:

- **-amin N, -cmin N, -mmin N**
  This will match files that have been accessed, had attributes changed or were modified (respectively) N minutes ago.
- **-atime N, -ctime N, -mtime N**
  This will match files that were accessed, had attributes changed or were modified N*24 hours ago.

For `-cmin N` and `-ctime N`, any attribute change will cause a match, including a change in permissions, reading or writing to the file. This makes these parameters especially powerful, since practically any operation involving the file will trigger a match.

The following example would match any file in the current directory which has been modified less than 24 hours ago and is bigger than 100 MiB:

```
$ find . -mtime -1 -size +100M
```
