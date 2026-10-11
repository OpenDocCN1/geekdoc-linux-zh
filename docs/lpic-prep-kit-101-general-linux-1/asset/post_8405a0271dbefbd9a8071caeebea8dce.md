
After you have the command line the way you want it, you need to create a file containing this command to be used to install it as a cron job. Using a text editor, create the file backups to contain the following line:

```
45 23 * * * tar czf MyBackup.tar.gz .
```

This will create an archive every night at 11:45 pm. If you want to save these, remember to move it before it is overwritten. You could add a command to do this in your cron job.

Now that you have your backup, you will want to test that you can restore files from it. Be sure that you are in your home directory when extracting files so they will be saved to the correct location. You also might want to use the w option to place tar in interactive mode so you can verify each file you want restored.

To select the file to extract from your archive, type the command tar xzvf MyBackup.tar.gz. This will prompt you for each file stored in the archive. To quit, press Ctrl-C.

## G

### Objectives Index

| **Objective** | **Subobjective** | **Page** |
| :--- | :--- | :--- |
| 3. GNU and UNIX Commands | 1. Work Effectively on UNIX Commands | 104-116 |
| | Interact with shells and commands using the command line. Includes typing valid commands and command sequences; defining, referencing, and exporting environment variables; using command history and editing facilities; invoking commands inside and outside the path; using command substitution; and applying commands recursively through a directory tree. | |
| | 2. Process Text Streams Using Text Processing Filters | 186-197 |
| | Send text files and output streams through text utility filters to modify the output in a useful way. Includes the use of standard UNIX commands found in the GNU texutils package such as `sed`, `sort`, `cut`, `expand`, `fmt`, `head`, `join`, `nl`, `od`, `paste`, `pr`, `split`, `tac`, `tail`, `tr`, and `wc`. | |
| | 3. Perform Basic File Management | 74-97 |
| | Use basic UNIX commands to copy and move files and directories. Perform advanced file management operations such as copying multiple files recursively and moving files that meet a wildcard pattern. Use simple and advanced wildcard specifications to refer to files. | |
| | 4. Use UNIX Streams, Pipes, and Redirects | |
| | Connect files to commands and commands to other commands to efficiently process textual data. Includes redirecting standard input, standard output, and standard error; piping one command’s output into another command; and sending output to **stdout** and a file using **tee**. | |
| | 5. Create, Monitor, and | |
| | Includes running jobs in the foreground and background, bringing a job from the background to the foreground and vice versa, monitoring active processes, sending signals to processes, and killing processes. Includes using commands such as **ps**, **top**, **kill**, **bg**, **fg**, and **jobs**. | |
| | 6. Modify Process Execution Priorities | |
| | Run a program with higher or lower priority; determine the priority of a process; change the priority of a running process. Includes the command **nice** and its relatives. | |
| | 7. Perform Searches of Text Files Using Regular Expressions | |
| | Includes creating simple regular expressions and using related tools such as **grep** and **sed** to perform searches. | |
| 4. Devices, Linux FileSystems, Filesystem Hierarchy Standard | 1. Create Partitions and Filesystems | |
| | Create disk partitions using **fdisk**; create a hard drive and other media filesystems using **mkfs**. | |
| | 2. Maintain the Integrity of Filesystems | |
| | Verify the integrity of filesystems, monitor free space and inodes, and fix simple filesystem problems. Includes commands such as **fsck**, **du**, and **df**. | |
| | 3. Control Filesystem Mounting and Unmounting | |
| | Mount and unmount filesystems manually, configure filesystem mounting on **bootup**, and configure user-mountable removable file systems. Includes managing the **/etc/fstab** file. | |
| | 4. Set and View Disk Quotas | |
| | Set up disk quotas for filesystems, edit user quotas, check user quotas, and generate reports of user quotas. Includes the **quota**, **edquota**, **repquota**, and **quotaon** commands. | |
| | 5. Use File Permissions to Control Access to Files | 210-215 |
| | Set permissions on files, directories, and special files; use special permission modes such as suid and sticky bit; use the group field to grant file access to workgroups; and change default file creation mode. Includes the chmod and umask commands. Requires an understanding of symbolic and numeric permissions. | |
| | 6. Manage File Ownership | 208-210 |
| | Change the owner or group for a file and control what group is assigned to new files created in a directory. Includes the chown and chgrp commands. | |
| | 7. Create and Change Hard and Symbolic Links | 139-142 |
| | Create hard and symbolic links, identify the hard links to a file, copy files by following or not following symbolic links, and use hard and symbolic links for efficient system administration. | |
| | 8. Find System Files and Place Files in the Correct Location | |
| | Understand the filesystem hierarchy standard, know standard file locations, know the purpose of various system directories, and find commands and files. Involves using the find, locate, which, and updatedb commands. Involves editing the /etc/updatedb.conf file. | |
| 6. Boot, Initialization, Shutdown, Runlevels | 1. Boot the System | 28-37 |
| | Guide the system through the booting process, including giving options to the kernel at boot time, and check the events in the log files. Involves using the dmesg (LILIO) command. Involves reviewing the /var/log/messages, /etc/lilo.conf, /etc/conf.modules, and /etc/modules.conf files. | |
| | 2. Change Runlevels and Shut Down or Reboot System | 30-40 |
| | Securely change the runlevel of the system, specifically to single-user mode; halt (shut down) the system; or reboot the system. Make sure to alert users beforehand and properly terminate processes. Involves using the shutdown and init commands. | |
| 8. Documentation | 1. Use and Manage Local System Documentation | |
| | Use and administer the man facility and the material in /usr/doc/. Includes finding relevant man pages, searching man page sections, finding commands and man pages related to the command, configuring access to man sources and the man system, using system documentation stored in /usr/doc/ and related places, and determining what documentation to keep in /usr/doc/. | |
| | 2. Find Linux Documentation on the Internet | |
| | Find and use Linux documentation at sources such as the Linux Documentation Project, vendor and third-party Web sites, newsgroups, newsgroup archives, and mailing lists. | |
| | 3. Write System Documentation | |
| | Write documentation and maintain logs for local conventions, procedures, configurations, configuration changes, file locations, applications, and shell scripts. | |
| | 4. Provide User Support | |
| | Provide technical assistance to users over the telephone, through email, and through personal contact. | |
| 11. Administrative Tasks | 1. Manage Users and Group Accounts and Related System Files | |
| | Add, remove, and suspend user accounts; add and remove groups; change user and group information in passwd and group databases; and create special-purpose and limited accounts. Includes using the useradd, userdel, groupadd, gpasswd, passwd, filepasswd, group, shadow, and gshadow commands. | |
| | 2. Tune the User Environment and System Environment Variables | |
| | Modify global and user profiles to set environment variables, maintain skel directories for new user accounts, and place proper commands in the path. Involves editing /etc/profile and /etc/skel/. | |
| | 3. Configure and Use System Log Files to Meet Administrative and Security Needs | |
| | Configure the type and level of information logged, manually scan log files for notable activity, arrange for automatic rotation and archiving of logs, and track down problems noted in logs. Involves editing /etc/syslog.conf. | |
| | 4. Automate System Administration Tasks by Scheduling Jobs to Run in the Future | 232-239 |
| | Use **cron** to run jobs at regular intervals, use **at** to run jobs at a specific time, manage **cron** and **at** jobs, and configure user access to **cron** and **at** services. | |
| | 5. Maintain an Effective Data Backup Strategy | 255-280 |
| | Plan a backup strategy, back up filesystems automatically to various media, perform partial and manual backups, verify the integrity of backup files, and partially or fully restore backups. | |
