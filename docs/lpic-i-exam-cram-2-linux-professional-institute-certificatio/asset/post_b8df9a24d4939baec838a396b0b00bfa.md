
To restrict the output to just the regular files in the current directory, use the following command:

```
du *
4   anaconda-ks.cfg
20  install.log
4   install.log.syslog
```

To see the current directory and all below with KB/MB/GB human-readable output, use the following command:

```
du -h
24K   ./.gconfd
8.0K  ./.gstremer
6.0K  ./.gconf/desktop/gnome/applications/window_manager
12K   ./.gconf/desktop/gnome/applications
8.0K  ./.gconf/desktop/gnome/file_views
8.0K  ./.gconf/desktop/gnome
28K   ./.gconf/desktop
... Output removed
```

To view the space used by all files on a given directory tree, such as the /home user's tree, use this command:

```
du -sh /home
```

Typical output would look like this:

```
404 MB    /home
```

It's very important when using du to not traverse NFS systems across the network, causing extra traffic and annoying router users. To restrict your query to the local system only, use the following:

```
du -shx /home
22M    /home
```

Without the x option, (which restricts du to the local system) a remotely mounted user's home directory or attached separate disk drive is shown in the output. Therefore, you should know from which drive and system the data is shown.

## Using df

The df command is different from the du command: It can't show a set of files disk usage, unless that set of files is an entire mounted file system.

The df command displays used and available disk space for all mounted file systems, on a per-file system basis (shown here with the -h human readable output option) such as

```
df -h
Filesystem     Size  Used Avail Use% Mounted on
/dev/sda2       5.5G  1.8G  3.5G  34% /
/dev/sda1        99M  9.3M  85M  10% /boot
none            62M   0   62M   0% /dev/shm
/dev/sdb8       966M  38M  909M   4% /data
```

Notice that df works only on mounted file systems, and that the output includes

- The size of the partition
- The size used in MB or GB
- The size available in MB or GB
- The percent used
- Where the device is mounted

To view disk-free statistics on local-only file systems, (excluding NFS and other remote mounts) use the following command:

```
df -l
```

To see the disk utilization statistics expressed in KB, use this command:

```
df -k
Filesystem    1K-blocks    Used Available Use% Mounted on
/dev/sda2      5708320  1794004   3624344  34% /
/dev/sda1       101089     9426    66444  10% /boot
none            62996        0    62996   0% /dev/shm
/dev/sdb8      988212   38180   929952   4% /home/data
```

Finally, to see the amount of the disk’s free and used inodes expressed in disk utilization statistics, use the following command:

```
df -i
Filesystem    Inodes IUsed  IFree  IUse% Mounted on
/dev/sda2      725760  104049  621711  15% /
/dev/sda1       26104      41  26063   1% /boot
none            15749       1  15748   1% /dev/shm
/dev/sdb8      125896     889  124807   1% /home/data
```

Notice that the number of inodes total, used, free, and percent used is shown on a file system-by-file system basis. This option is incredibly useful for busy sysadmins who are worried about running out of space or inodes.

> **The du and df** commands are prominently featured on the exams, particularly questions about the output of each and what is shown for various options. Expect to see questions that have the keywords disk utilization and amount of free space or words to that effect.

![](img/49f4f38f3aec011238fa50f89e643db3_168_0.png)

## Exam Prep Questions

1. You are configuring your /etc/fstab file and want to have a file system mountable by non-root users. Which option in which column would you use to accomplish this?

- A. owner in the third column
- B. owner in the fifth column
- C. noauto in the fourth column
- D. user in the fourth column

Answer D is correct because the fourth column is the options column and the user option is the proper one to use. Answers A and B include valid options but are in the wrong column. Answer C is the wrong option in the right column.

2. You are troubleshooting your Linux machine after an unexplained crash. The automated file system check fails with a message to perform a check manually. What's the most important thing to make certain of for the affected file system before initiating the manual check?

- A. It should be unmounted.
- B. It should be mounted read-write.
- C. It should be in noauto mode.
- D. The user=root option should be set.

Answer A is correct because the file system should be unmounted if possible, mounted read-only if not. Answer B is incorrect because mounting it read-write would cause errors in the fsck process. Answer C is incorrect because there isn't a noauto mode, although there is a noauto option. Answer D is incorrect because the user being set to something in options doesn't affect the fsck process.

3. You are installing a Linux server that will primarily hold users' data. If you could place two directory trees on a separate drive, which would be the most effective choice? (Choose two.)

- A. /tmp
- B. /var
- C. /home
- D. /data

Answers B and C are correct because the highest traffic partitions in the choices are /home (users data) and /var (log files, print spools, Web, and FTP). Answer A is incorrect because on a user file server, /tmp isn't as heavily used as it would be on a developer station. Answer D is incorrect because anything at all could be in a directory tree named /data, whereas the /home directory tree is almost certainly user data.

4. You require your system to check a particular file system every 50 times the file system is mounted. Which command would you use to make this change?

- A. `debugfs`
- B. `dumpe2fs`
- C. `tune2fs`
- D. `setfs`

Answer C is correct because the maximum mount count option can be set with the `tune2fs` command. Answer A is incorrect because the `debugfs` command manipulates the file system modes and contents but not the needed parameter. Answer B is incorrect because the `dumpe2fs` command shows only parameters for the file system. Answer D is incorrect because the `setfs` command doesn't exist.

5. A user reports that one of his fellow users is hogging all the disk space on their shared server. Which command would you use to show that system's disk statistics for its mounted file systems?

- A. `dir`
- B. `df`
- C. `du`
- D. `ls`

Answer B is correct because the `df` command shows the disk statistics for mounted file systems. Answer A is incorrect because `dir` is only an alias for the `ls` command. Answer C is incorrect because the `du` command can show the space used by files, but not disk statistics like `df` can. Answer D is incorrect because the `ls` command can show file sizes but not disk statistics.

6. What is the device name of the third SCSI device on a Linux system? Fill in the blank with the full path and filename of the device:

![](img/49f4f38f3aec011238fa50f89e643db3_170_0.png)

The correct answer is /dev/sdc. There are no alternative answers.

7. Which portion of a file's information is not stored in the `inode` or `data blocks`?

- A. Link count
- B. Link permissions
- C. Filename
- D. Owner

Answer C is correct because the filename is not stored with the `inode` or in the data location for the file; it occurs only in the directory file that contains the filename entry. Answer A is incorrect because the link count affects only hard links and is shown by the `stat` command. Answer B is incorrect because link permissions affect only a symbolic link, and the symbolic link permissions are kept in the links inode. Answer D is incorrect because the ownership information is kept in the inode for the file.

8. Which command is used to alter the maximum mount count so an **ext3** file system isn't checked every 20 mounts by default?

- A. **fsck**
- B. **mkfs.ext3**
- C. **hdparm**
- D. **tune2fs**

Answer D is correct because the `tune2fs -c 0` command changes a file system's maximum mount count to not have it checked automatically. Answer A is incorrect because the **fsck** command can't change the maximum mount count. Answer B is incorrect because the `mkfs.*` tools are for creating file systems, and even though they can set the maximum mount count at file system creation, using these tools on existing file systems would destroy the file system. Answer C is incorrect because, although **hdparm** is good for changing parameters, the `tune2fs` command is the best choice for this task.

9. When upgrading a system that has multiple data partitions of the **ext2** file system type, which of the following would represent the least disruptive journalling file system to upgrade them with?

- A. ext3
- B. **ReiserFS**
- C. **JFS**
- D. **XFS**

Answer A is correct because the **ext3** file system type does not require any reformatting to upgrade an **ext2** file system. Answers B, C, and D are incorrect because they require backing up the file system data, formatting with the new advanced file system, and restoring the data.

10. Which utility on your system can display the number of free and used inodes as a total and percentage?

- A. `ls -li`
- B. `du -sh`
- C. `df -i`
- D. `find -inum`

Answer C is correct because the `df` command has an option to query the number and percentage of inodes used and free for all mounted file systems. Answer A is incorrect because the `ls -li` command shows only groups of file object inode information, not totals. Answer B is incorrect because the `du -sh` command doesn't show inode percentages, just object sizes and size totals. Answer D is incorrect because `find -inum` searches for a specific inode but does not show totals or percentages.
