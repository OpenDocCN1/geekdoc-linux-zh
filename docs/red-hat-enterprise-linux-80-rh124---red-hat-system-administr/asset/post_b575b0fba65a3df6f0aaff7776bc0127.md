
# Evaluation

On workstation, run the lab net-review grade script to confirm success on this lab.

```
[student@workstation ~]$ lab net-review grade
```

# Finish

On workstation, run the lab net-review finish script to finish this lab.

```
[student@workstation ~]$ lab net-review finish
```

This concludes the lab.

# SUMMARY

In this chapter, you learned:

- The TCP/IP network model is a simplified, four-layered set of abstractions that describes how different protocols interoperate in order for computers to send traffic from one machine to another over the Internet.
- IPv4 is the primary network protocol used on the Internet today. IPv6 is intended as an eventual replacement for the IPv4 network protocol. By default, Red Hat Enterprise Linux operates in dual-stack mode, using both protocols in parallel.
- NetworkManager is a daemon that monitors and manages network configuration.
- The nmcli command is a command-line tool for configuring network settings with NetworkManager.
- The system's static host name is stored in the /etc/hostname file. The hostname command is used to modify or view the status of the system's host name and related settings.
The hostname command displays or temporarily modifies the system's host name.

# CHAPTER 13

# ARCHIVING AND TRANSFERRING FILES

# GOAL

Archive and copy files from one system to another.

# OBJECTIVES

- Archive files and directories into a compressed file using tar, and extract the contents of an existing archive.
- Transfer files to or from a remote system securely using SSH.
- Synchronize the contents of a local file or directory with a copy on a remote server.

# SECTIONS

- Managing Compressed Tar (Guided Exercise)
- Transferring Files Between Systems (Guided Exercise)
- Synchronizing Files Between Systems (Guided Exercise)

# LAB: Archiving and Transferring Files

# MANAGING COMPRESSED ARCHIVES

# OBJECTIVES

After completing this section, you should be able to archive files and directories into a compressed file using tar, and extract the contents of an existing archive.

# THE TAR COMMAND

Archiving and compressing files are useful when creating backups and transferring data across a network. One of the oldest and most common commands for creating and working with backup archives is the tar command. With tar, you can gather large sets of files into a single file (archive). A tar archive is a structured sequence of file data with metadata about each file and an index so that individual files can be extracted. The archive can be compressed using gzip, bzip2, or xz compression.

# SELECTED OPTIONS

tar command options are divided into operations (the action you want to take), general options and compression options. The table below shows common options, long version of options, and their description:

## Overview of tar Operations

| OPTION | DESCRIPTION |
| --- | --- |
| -c, --create | Create a new archive. |
| -x, --extract | Extract from an existing archive. |
| -t, --list | List the contents of an archive. |

## Selected tar General Options

| OPTION | DESCRIPTION |
| --- | --- |
| -v, --verbose | Verbose. Shows which files get archived or extracted. |
| -f, --file= | File name. Name of the archive to use or create. |
| -p, --preserve-permissions | Preserve the permissions of files and directories when extracting an archive, without umask. |

## Overview of tar Compression Options

| OPTION | DESCRIPTION |
| --- | --- |
| -z, --gzip | Use gzip compression (.tar.gz). |
| -j, --bzip2 | Use bzip2 compression (.tar.bz2). bzip2 typically achieves a better compression ratio than gzip. |
| -J, --xz | Use xz compression (.tar.xz). xz compression typically achieves a better compression ratio than bzip2. |

# LISTING OPTIONS OF THE tar COMMAND

The tar command executes one of the following:

- Use the -c or --create to create an archive.
- Use the -t or --list to list the contents of an archive.
- Use the -x or --extract to extract an archive.

Other commonly used options:

- Use the -f or --file option with a file name as an argument of the archive to operate.
- Use the -v or --verbose option for verbosity; useful to see files get added or extracted from the archive.

> NOTE
The tar command actually supports old-letter options with no leading -. It is still commonly encountered, and you might run into this syntax when working with other people's instructions or commands. The info 'old options' command discusses how this differs from normal short options in detail. You can ignore old options and focus on the standard short and long options syntax.

# ARCHIVING FILES AND DIRECTORIES

The first option to use when creating a new archive is the c option, followed by the f option, a single space, the file name of the archive to be created, and finally the list of files and directories that should get added to the archive. The archive is created in the current directory unless specified otherwise.

> WARNING
Before creating a tar archive, verify that there is no other archive in the directory with the same name as the new archive to be created. The tar command overwrites an existing archive without warning.

The following command creates an archive named archive.tar with the contents of file1, file2 and file3 in the user's home directory.

```
[user@host ~]$ tar -cf archive.tar file1 file2 file3
```

# CHAPTER 12 | Archiving and transferring files

```
[user@host ~]$ ls archive.tar
archive.tar
```

The tar command can also be executed using the long version options.

```
[user@host ~]$ tar --file=archive.tar --create file1 file2 file3
```

> NOTE
When archiving by absolute path names, the leading / of the path is removed from the file by default. Removing the leading / the path help users to avoid overwriting important files when extracting the archive. The tar command extracts files relative to the current working directory.

For tar to be able to archive the selected files, it is mandatory that the user executing the tar command can read the files. For example, creating a new archive of the /etc folder and all of its content requires root privileges, because only the root user is allowed to read all of the files in the /etc directory. An unprivileged user can create an archive of the /etc directory, but archive omits files that do not include read permission for the user, and its omits directories which do not read and execute permission for the user.

To create the tar archive named /root/etc.tar, with the /etc directory as content as root:

```
[root@host ~]# tar -cf /root/etc.tar /etc
Removing leading '/' from member names
[root@host ~]#
```

> IMPORTANT
Some advanced permissions that we have not covered in this course, such as ACLs and SELinux contexts, are not automatically stored in a tar archive. Use the --xattr option when creating an archive to store extended attributes.

# LISTING CONTENTS OF AN ARCHIVE

The t option directs tar to list the contents of an archive. Use the f option with the name of the archive to be queried. For example:

```
[root@host ~]# tar -tf /root/etc.tar
etc/
etc/fstab
etc/crypt
etc/mtab
```

# EXTRACTING FILES FROM AN ARCHIVE

A archive should usually be extracted in an empty directory to ensure it does not overwrite any existing files. When root extracts an archive, the tar command preserves the original user ownership. To restore files from the /etc.tar archive to the /root/backup directory, run:

In this example, an archive named, /root/myscripts.tar, is extracted in the /root/scripts directory while preserving the permissions of the extracted files:

```
[root@host ~]# mkdir /root/scripts
[root@host ~]# cd /root/scripts
[root@scripts]# tar -xpf /root/myscripts.tar
```

# CREATING A COMPRESSED ARCHIVE

The tar command supports three compression methods. There are three different compression methods supported by the tar command. The gzip compression is the fastest and oldest one and is widely available across all distributions and even across platforms. bzip2 compression smaller archive files compared to gzip is less widely available than gzip, while the xz compression method is relatively new, but usually offers the best compression ratio of the methods available.

> NOTE
The effectiveness of any compression algorithm depends on the type of data that is compressed. Data files that are already compressed, as compressed picture formats or RPM files, usually lead to a low compression ratio.

It is good practice to use a single top-level directory, which can contain other directories and files, to simplify the extraction of the files in an organized way.

Use one of the following options to create a compressed archive:

- -z or -gzip for compression (filename.tar.gz or filename.tgz)
- -j or -bzip2 for bzip2 compression (filename.tar.bz2)
- -J or -xz for xz compression (filename.tar.xz)

To create a gzip compressed archive named /root/etcbackup.tar.gz, with the contents of the /etc directory on host:
