
This will send messages to the console. However, you will need to notify the syslogd daemon of the changes. How can you do this?

You can reboot your computer in order to force the syslogd daemon to reread the configuration file. However, a better way would be to enter the command

```bash
kill -SIGHUP $(cat /var/run/syslogd.pid)
```

Now any emergency messages will be sent to the console.

Look at the contents of the directory /var/log. Do you see older log files being saved here? How is this being done? Chances are this is the result of the logrotate command.

Check out the /etc/logrotate.conf file. What logs are being rotated? How frequently? How many old logs are being kept? Many distributions also install a cron job to run logrotate. Look in the /etc/cron.daily directory for the logrotate job. You can view it using cat or a text editor. Just be careful not to make any changes.

# Lab 11: Backup and Recovery

For this exercise, you will devise a backup strategy and implement it. You also will perform trial restores to ensure that your plan will work in case of a disaster.

First, answer the following three questions:

- What are you going to back up?
- How often will you back up?
- What media will you use for your backup?

The answers will vary from system to system. If you have a single-user system, you will probably back up the entire system whenever you make changes and back up your files on a daily basis. If it is a multiuser system, however, you will want to make complete backups on a regular basis as well as daily backups of user files.

For this exercise, you will create a backup of your home directory on a daily basis. The first step is to construct and test the commands necessary to create your backup.

For this you will use tar to create a compressed archive. You will save this to your home directory. Later you will want to modify this to save the archive to your backup device, such as a tape drive.

Type the following:

```bash
cd
tar czf MyBackup.tar.gz .
```

After you have the command line the way you want it, you need to create a file containing this command to be used to install it as a cron job. Using a text editor, create the file backups to contain the following line:

```bash
45 23 * * * tar czf MyBackup.tar.gz .
```

This will create an archive every night at 11:45 pm. If you want to save these, remember to move it before it is overwritten. You could add a command to do this in your cron job.

Now that you have your backup, you will want to test that you can restore files from it. Be sure that you are in your home directory when extracting files so they will be saved to the correct location. You also might want to use the w option to place tar in interactive mode so you can verify each file you want restored.

To select the file to extract from your archive, type the command `tar xzvf MyBackup.tar.gz`. This will prompt you for each file stored in the archive. To quit, press Ctrl-C.

![](img/8c0f494a2e9a2273fb49af52267f311e_337_0.png)

# Objectives Index

## 3. GNU and UNIX Commands

| Objective | Subobjective | Page |
| :--- | :--- | :--- |
| 1. Work Effectively on UNIX Commands | Interact with shells and commands using the command line. Includes typing valid commands and command sequences; defining, referencing, and exporting environment variables; using command history and editing facilities; invoking commands inside and outside the path; using command substitution; and applying commands recursively through a directory tree. | 104-116 |
| 2. Process Text Streams Using Text Processing Filters | Send text files and output streams through text utility filters to modify the output in a useful way. Includes the use of standard UNIX commands found in the GNU textutils package such as sed, sort, cut, expand, fmt, head, join, nl, od, paste, pr, split, tac, tail, tr, and wc. | 186-197 |
| 3. Perform Basic File Management | Use basic UNIX commands to copy and move files and directories. Perform advanced file management operations such as copying multiple files recursively and moving files that meet a wildcard pattern. Use simple and advanced wildcard specifications to refer to files. | 74-97 |
| 4. Use UNIX Streams, Pipes, and Redirects | Connect files to commands and commands to other commands to efficiently process textual data. Includes redirecting standard input, standard output, and standard error; piping one command's output into another command; and sending output to `stdout` and a file using `tee`. | 198-200 |
| 5. Create, Monitor, and Manage Jobs | Includes running jobs in the foreground and background, bringing a job from the background to the foreground and vice versa, monitoring active processes, sending signals to processes, and killing processes. Includes using commands such as `ps`, `top`, `kill`, `bg`, `fg`, and `jobs`. | 117-122 |
| 6. Modify Process Execution Priorities | Run a program with higher or lower priority; determine the priority of a process; change the priority of a running process. Includes the command `nice` and its relatives. | 118-120 |
| 7. Perform Searches of Text Files Using Regular Expressions | Includes creating simple regular expressions and using related tools such as `grep` and `sed` to perform searches. | 87-92 |

## 4. Devices, Linux Filesystems, Filesystem Hierarchy Standard

| Objective | Subobjective | Page |
| :--- | :--- | :--- |
| 1. Create Partitions and Filesystems | Create disk partitions using `fdisk`; create a hard drive and other media filesystems using `mkfs`. | 46-55 |
| 2. Maintain the Integrity of Filesystems | Verify the integrity of filesystems, monitor free space and inodes, and fix simple filesystem problems. Includes commands such as `fsck`, `du`, and `df`. | 45-72 |
| 3. Control Filesystem Mounting and Unmounting | Mount and unmount filesystems manually, configure filesystem mounting on bootup, and configure user-mountable removable filesystems. Includes managing the `/etc/fstab` file. | 130-134 |
| 4. Set and View Disk Quotas | Set up disk quotas for filesystems, edit user quotas, check user quotas, and generate reports of user quotas. Includes the `quota`, `edquota`, `repquota`, and `quotaon` commands. | 134-139 |
| 5. Use File Permissions to Control Access to Files | Set permissions on files, directories, and special files; use special permission modes such as suid and sticky bit; use the group field to grant file access to workgroups; and change default file creation mode. Includes the chmod and umask commands. Requires an understanding of symbolic and numeric permissions. | 210-215 |
| 6. Manage File Ownership | Change the owner or group for a file and control what group is assigned to new files created in a directory. Includes the chown and chgrp commands. | 208-210 |
| 7. Create and Change Hard and Symbolic Links | Create hard and symbolic links, identify the hard links to a file, copy files by following or not following symbolic links, and use hard and symbolic links for efficient system administration. | 139-142 |
| 8. Find System Files and Place Files in the Correct Location | Understand the filesystem hierarchy standard, know standard file locations, know the purpose of various system directories, and find commands and files. Involves using the find, locate, which, and updatedb commands. Involves editing the /etc/updatedb.conf file. | 142-145 |

## 6. Boot, Initialization, Shutdown, Runlevels

| Objective | Subobjective | Page |
| :--- | :--- | :--- |
| 1. Boot the System | Guide the system through the booting process, including giving options to the kernel at boot time, and check the events in the log files. Involves using the dmesg (-l) command. Involves reviewing the /var/log/messages, /etc/lilo.conf, /etc/conf.modules, and /etc/modules.conf files. | 28-37 |
| 2. Change Runlevels and Shut Down or Reboot System | Securely change the runlevel of the system, specifically to single-user mode; halt (shut down) the system; or reboot the system. Make sure to alert users beforehand and properly terminate processes. Involves using the shutdown and init commands. | 30-40 |

## 8. Documentation

| Objective | Subobjective | Page |
| :--- | :--- | :--- |
| 1. Use and Manage Local System Documentation | Use and administer the man facility and the material in /usr/doc/. Includes finding relevant man pages, searching man page sections, finding commands and man pages related to the command, configuring access to man sources and the man system, using system documentation stored in /usr/doc/ and related places, and determining what documentation to keep in /usr/doc/. | 8-18 |
| 2. Find Linux Documentation on the Internet | Find and use Linux documentation at sources such as the Linux Documentation Project, vendor and third-party Web sites, newsgroups, newsgroup archives, and mailing lists. | 16-18 |
| 3. Write System Documentation | Write documentation and maintain logs for local conventions, procedures, configurations, configuration changes, file locations, applications, and shell scripts. | 20-21 |
| 4. Provide User Support | Provide technical assistance to users over the telephone, through email, and through personal contact. | 21-22 |

## 11. Administrative Tasks

| Objective | Subobjective | Page |
| :--- | :--- | :--- |
| 1. Manage Users and Group Accounts and Related System Files | Add, remove, and suspend user accounts; add and remove groups; change user and group information in passwd and group databases; and create special-purpose and limited accounts. Includes using the useradd, userdel, groupadd, gpasswd, passwd, filepasswd, group, shadow, and gshadow commands. | 156-164 |
| 2. Tune the User Environment and System Environment Variables | Modify global and user profiles to set environment variables, maintain skel directories for new user accounts, and place proper commands in the path. Involves editing /etc/profile and /etc/skel/. | 174-177 |
| 3. Configure and Use System Log Files to Meet Administrative and Security Needs | Configure the type and level of information logged, manually scan log files for notable activity, arrange for automatic rotation and archiving of logs, and track down problems noted in logs. Involves editing /etc/syslog.conf. | 239-243 |
