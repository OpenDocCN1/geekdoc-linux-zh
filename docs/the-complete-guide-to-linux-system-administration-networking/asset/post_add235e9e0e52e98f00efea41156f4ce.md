
## 1.102.6 Use Red Hat Package Manager (RPM)

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 8 | Candidates should be able to perform package management under Linux distributions that use RPMs for package distribution. This objective includes being able to install, reinstall, upgrade, and remove packages, as well as obtain status and version information on packages. This objective also includes obtaining package information such as version, status, dependencies, integrity, and signatures. Candidates should be able to determine what files a package provides, as well as find which package a specific file comes from. Key files, terms, and utilities include: /etc/rpmrc, /usr/lib/rpm/*, rpm, grep. | Chapter 10, "Managing Packages" |

## Topic 103 GNU and UNIX Commands

## 1.103.1 Work on the Command Line

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | Candidates should be able to interact with shells and commands using the command line. This includes typing valid commands and command sequences; defining, referencing, and exporting environment variables; using command history and editing facilities; invoking commands in the path and outside the path; using command substitution; applying commands recursively through a directory tree; and using man to find out about commands. Key files, terms, and utilities include: bash, echo, env, exec, export, man, pwd, set, unset, ~/.bash_history, ~/.profile. | Chapter 1, "Starting to Use Linux" and "Exploring the File System" |

|  |  | Chapter 3, throughout |

## 1.103.2 Process Text Streams Using Filters

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 6 | Candidates should be able to apply filters to text streams. Tasks include sending text files and output streams through text utility filters to modify the output, and using standard UNIX commands found in the GNU textutils package. Key files, terms, and utilities include: cat, cut, expand, fmt, head, join, nl, od, paste, pr, sed, sort, split, tac, tail, tr, unexpand, uniq, wc. | Chapter 5, "Manipulating Files" |

## 1.103.3 Perform Basic File Management

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | Candidates should be able to use the basic UNIX commands to copy, move, and remove files and directories. Tasks include advanced file management operations such as copying multiple files recursively, removing directories recursively, and moving files that meet a wildcard pattern. This includes using simple and advanced wildcard specifications to refer to files, as well as using find to locate and act on files based on type, size, or time. Key files, terms, and utilities include: cp, find, mkdir, mv, ls, rm, rmdir, touch, file globbing. | Chapter 1, "Exploring the File System" |
|  |  | Chapter 4, "Introducing the File System" |
|  |  | Chapter 5, "Regular Expressions" |

## 1.103.4 Use Streams, Pipes, and Redirects

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | Candidates should be able to redirect streams and connect them in order to process textual data efficiently. Tasks include redirecting standard input, standard output, and standard error, piping the output of one command to the input of another command, using the output of one command as arguments to another command, and sending output to both stdout and a file. Key files, terms, and utilities include: tee, xargs, <, <<, >, >>, |, ` | Chapter 3, "Data Redirection" |

## 1.103.5 Create, Monitor, and Kill Processes

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | Candidates should be able to manage processes. This includes knowing how to run jobs in the foreground and background, bringing a job from the background to the foreground and vice versa, starting a process that will run without being connected to a terminal, and signaling a program to continue running after logout. Tasks also include monitoring active processes, selecting and sorting processes for display, sending signals to processes, killing processes, and identifying and killing X applications that did not terminate after the X session closed. Key files, terms, and utilities include: &, bg, fg, jobs, kill, nohup, ps, top. | Chapter 6, "Defining Processes" and "Managing Linux Processes" |

## 1.103.6 Modify Process Execution Priorities

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | Candidates should be able to manage process execution priorities. Tasks include running a program with higher or lower priority, determining the priority of a process, and changing the priority of a running process. Key files, terms, and utilities include: nice, ps, renice, top. | Chapter 6, "Managing Linux Processes" |

## 1.103.7 Search Text Files Using Regular Expressions

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | Candidates should be able to manipulate files and text data using regular expressions. This objective includes creating simple regular expressions containing several notational elements. It also includes using regular expression tools to perform searches through a file system or file content. Key files, terms, and utilities include: grep, regexp, sed. | Chapter 5, "Manipulating Files" |

## 1.103.8 Perform Basic File-editing Operations Using vi

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | Candidates must be able to edit text files using vi. This objective includes vi navigation, basic vi nodes, inserting, editing, deleting, copying, and finding text. Key files, terms, and utilities include: vi, /, ?, h, j, k, l, G, H, L, i, c, d, dd, p, o, a, ZZ, :w!, :q!, :e!, :! | Chapter 3, "Editing Text with vi" |
|  |  | Chapter 5, "More Advanced Text Editing" |

## Topic 104 Devices, Linux File Systems, and File System Hierarchy Standard

## 1.104.1 Create Partitions and File Systems

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | Candidates should be able to configure disk partitions and then create file systems on media such as hard disks. This objective includes using various mkfs commands to set up partitions to various file systems, including ext2, ext3, reiserfs, vfat, and xfs. Key files, terms, and utilities include: fdisk, mkfs. | Chapter 4, "Introducing the File System" |
|  |  | Chapter 8, "Configuring Disk Space" |
|  |  | Chapter 10, "Understanding the File System" |

## 1.104.2 Maintain the Integrity of File Systems

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | Candidates should be able to verify the integrity of file systems, monitor free space and inodes, and repair simple file system problems. This objective includes the commands required to maintain a standard file system, as well as the extra data associated with a journaling file system. Key files, terms, and utilities include: du, df, fsck, e2fsck, mke2fs, debugfs, dumpe2fs, tune2fs. | Chapter 10, "Understanding the File System" |

## 1.104.3 Control Mounting and Unmounting File Systems

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | Candidates should be able to configure the mounting of a file system. This objective includes the ability to manually mount and unmount file systems, configure file system mounting on bootup, and configure user-mountable removable file systems such as tape drives, floppies, and CDs. Key files, terms, and utilities include: /etc/fstab, mount, umount. | Chapter 4, "Introducing the File System" |
|  |  | Chapter 10, "Understanding the File System" |

## 1.104.4 Managing Disk Quotas

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | Candidates should be able to manage disk quotas for users. This objective includes setting up a disk quota for a file system, editing, checking, and generating user quota reports. Key files, terms, and utilities include: quota, edquota, repquota, quotaon. | Chapter 10, "Understanding the File System" |

## 1.104.5 Use File Permissions to Control Access to Files

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | Candidates should be able to control file access through permissions. This objective includes access permissions on regular and special files as well as directories. Also included are access modes such as suid, sgid, and the sticky bit, the use of the group field to grant file access to workgroups, the immutable flag, and the default file creation mode. Key files, terms, and utilities include: chmod, umask, chattr. | Chapter 4, "File Permissions" |
|  |  | Chapter 11, "Complex File Permissions" |

## 1.104.6 Manage File Ownership

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | Candidates should be able to control user and group ownership of files. This objective includes the ability to change the user and group owner of a file as well as the default group owner for new files. Key files, terms, and utilities include: chmod, chown, chgrp. | Chapter 4, "File Permissions" |

## 1.104.7 Create and Change Hard and Symbolic Links

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | Candidates should be able to create and manage hard and symbolic links to a file. This objective includes the ability to create and identify links, copy files through links, and use linked files to support system administration tasks. Key files, terms, and utilities include: ln. | Chapter 4, "Introducing the File System" |
