
## bzip2

Another commonly used compression utility is `bzip2`. As with the `gzip` and `compress` utilities, the permissions, ownership, and file modification times remain intact. The original file is replaced with a compressed file of the same name ending in the `.bz2` extension. These files can be uncompressed using the `bunzip2` utility. The options that can be used with the `bzip2` utility are shown in Table 6-20.

### Table 6-20: Options Used with bzip2

| Option | Use |
| :--- | :--- |
| `-c` | Results are sent to standard output while the file is left intact. This ensures that the original file is preserved. |
| `-d` | Decompresses the specified file. |
| `-z` | Compresses the specified file. |
| `-t` | Perform a trial compression of the specified file. |
| `-f` | Forces files to be overwritten. |
| `-k` | Keeps the original file when compressing or decompressing. |
| `-q` | Suppresses warning messages. |
| `-V` | Displays version information. |
| `-v` | Verbosely displays information. |

The bzip2 utility uses the same syntax as the other compression utilities. The correct syntax is as follows:

```
bzip2 -options FILENAME
```

## Managing Quotas

### 2.4 Devices, Linux File Systems, Filesystem Hierarchy Standard

- **Set and view disk quota.** Setup disk quota for a filesystem, edit user quota, check user quota, generate reports of user quota. Includes quota, edquota, repquota, quotaon, quotaoff commands.

Another part of managing files and directories on a Linux system involves working with *quotas*. Users can quickly fill system drives, and it seems that regardless of the amount of disk space installed on a system, that space is never enough. To prevent the users on your system from using all of the available space to store personal files, including large image and music files, you can use disk quotas. Quotas place a limit on the amount of disk space any single user can use. If the user reaches the quota, he or she is unable to create new files.

Linux includes several tools for managing quotas. The *quota, edquota, repquota*, and *quotaon* utilities work together to provide a total quota solution. Each of these utilities is covered in the sections below.

### quota

The *quota* utility is used to view information about disk usage and user quotas. Users are able to view information only for their own user account and groups, but the superuser can view this information for all users and groups. Quota information can be displayed for all file systems listed in `/etc/fstab`; this file contains information regarding whether quotas can be used on the various file systems. The files used to manage quotas are located in file system root and are *quota.user* for user accounts and *quota.group* for group quotas. These files must be created by the superuser and must be created with read and write permissions only for the superuser account. These files are not manually edited when working with quotas. Instead, the tools covered in the following sections are utilized when managing quotas. Quotas are specified at the partition level, which enables you to control which partitions use quotas and to set these quotas independently.

Understanding the relationship between user and group quotas is important. User and group quotas are set individually. When a user creates a new file, that user's account and group both have ownership of the file. If a user's group has exceeded its quota limit, the user will be unable to create new files, regardless of the user's account quota. This is important to remember when defining quotas. An example of the correct use of the quota utility is the following:

```
# quota angie
Disk quotas for user angie (uid 501): none
```

The quota utility has several options to specify which information is displayed. These options are covered in Table 6-21.

### Table 6-21: Options Used with quota

| Option | Use |
| :--- | :--- |
| -g | Displays group quota information. |
| -u | Displays user quota information. This is the default action. |
| -v | Displays quotas on file systems with no storage allocated. |
| -q | Displays information for file systems with usage exceeding the quota. |

### edquota

The edquota utility is used by the superuser to edit user and group quotas. The superuser uses this utility to set three different quota limits. The soft limit is a limit that can be exceeded for a period of time. The grace period is the period of time in which a user can exceed their soft limit. The hard limit is a limit at which a user can no longer create new files. The correct use of the edquota utility is shown below. In this example angie is given the same quota information as the jason account.

```
# edquota -p jason -u angie
```

The vi editor is the default editor used with the edquota utility. This utility writes the changes to the quota.user and quota.group files. You can use several options for editing quotas. These options are explained in Table 6-22.

### Table 6-22: Options Used with edquota

| Option | Use |
| :--- | :--- |
| -u | Specifies to edit the user quota. This is the default action. |
| -g | Specifies to edit the group quota. |
| -p user | Duplicates the quotas of the user specified for each user specified. |
| -t | Used to edit the grace period used for soft limits for each file system. |

### repquota

The repquota utility displays a summary of the disk usage and quotas for the specified file systems. The current number of files and amount of space (in kilobytes) for each user is displayed, along with any quotas created using edquota. Users on the system can use this utility for viewing quota information for their account; the superuser can view quota information for all users. Table 6-23 covers the options used with repquota.

### Table 6-23: Options Used with repquota

| Option | Use |
| :--- | :--- |
| -a | Displays information on all file systems indicated in /etc/fstab with quotas. |
| -v | Displays information for all quotas, even if there is no usage. |
| -g | Displays quota information for groups. |
| -u | Displays quota information for users. This is the default. |

Following is an example of output produced by the repquota command:

```
# repquota -v /
*** Report for user quotas on / (/)      Block limits   File limits
User  used soft hard grace used soft hard grace
root  --     8   0   0     1  0  0
```

### quotaon and quotaooff

The quotaon and quotaooff utilities are used to enable and disable file system quotas. The quota.user and quota.group files must exist before you can run the quotaon utility. Several options are available for used with both commands. The use of the option varies somewhat depending on whether the option is used with quotaon or quotaooff. The options and uses for both commands are shown in Table 6-24.

### Table 6-24: Options for quotaon and quotaooff

| Option | Use with quotaon | Use with quotaooff |
| :---- | :---- | :---- |
| -a | Enables quotas for all file systems in `/etc/fstab` that are configured with read/write quotas. | Disables quotas for all file systems listed in `/etc/fstab`. |
| -v | Displays a message for each file system with quotas enabled. | Displays a message for each file system affected. |
| -u | Enables user quotas; this is the default action. | Disables user quotas; this is the default action. |
| -g | Enables group quotas. | Disables group quotas. |

## Key Point Summary

File management is an important part of working with any system. Linux provides a variety of powerful tools that make this task easier and allow greater control over files. These tools are extremely important to understand for daily work with Linux systems and essential for the exams. Be sure that you are familiar with all points in the summary presented here before scheduling your exams.

- Directory changing is done with the `cd` command.
- Directory contents are displayed using `ls`.
- The `file` command is useful for examining files to determine file type.
- The `touch` command is used to create files and change time stamps on existing files.
- Files are copied with `cp` and moved or renamed with `mv`.
- The `dd` command is useful for copying and converting files simultaneously.
- The `rm` command is used to delete files.
- The `mkdir` command creates new directories.
- The `/etc` directory contains configuration files; the `/etc/skel` directory contains files copied to each user's home directory.
- The `/usr` directory contains `/usr/bin` with binaries executed by users, `/usr/sbin` with binaries executed by root user, `/usr/local` with applications that aren't part of the Linux operating system, `/usr/local/bin` with third-party software used by users, and `/usr/local/sbin` with software used by the root user that is installed after the initial operating system installation.
