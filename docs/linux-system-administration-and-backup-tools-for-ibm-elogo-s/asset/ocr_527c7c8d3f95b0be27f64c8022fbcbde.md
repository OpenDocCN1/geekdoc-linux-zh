Select OK to continue and you will see a recovery similar to Figure 200.

```
Terminal
Permission  Uid Gid Bytes  Last Modified             Filename
-xr-xr-x   0/0    203807 Aug 10 20:41 1999 /usr/src/linux-2 2.10/System map
-xr-xr-x   0/0    199497 Aug 10 21:06 1999 /usr/src/linux-2 2.10/vmem map
-rw-r--r-- 0/0    31363 Sep 30 23:59 1999 /usr/src/linux-2 2.10/include/li
-rw-r--r-- 0/0     7295 Jan 26 18:19 1999 /usr/src/linux-2 2.10/include/li
-rw-r--r-- 0/0    52058 Feb 05 12:13 1999 /usr/src/linux-2 2.10/include/li
-rw-r--r-- 0/0     4620 Apr 24 00:20 1999 /usr/src/linux-2 2.10/include/li
-xr-xr-x   0/0     2760 Mar 11 14:33 1999 /usr/src/linux-2 2.10/include/li
-xr-xr-x   0/0    10324 Apr 24 00:26 1999 /usr/src/linux-2 2.10/include/li
-xr-xr-x   0/0     4472 Jan 26 18:19 1999 /usr/src/linux-2 2.10/include/li
-rw-r--r-- 0/0    28710 Feb 24 01:01 1998 /usr/src/linux-2 2.10/include/li
-rw-r--r-- 0/0    13648 Dec 12 13:58 1998 /usr/src/linux-2 2.10/include/li
-rw-r--r-- 0/0     2674 Jul 30 14:17 1998 /usr/src/linux-2 2.10/include/li
```

Figure 200. Recovery report

Your files were recovered successfully!

# 7.2.5 Master and incremental backups

Usually system administrators perform called master and incremental backups. The master backup is a backup of all files on the system. Incremental backup is a backup of only those files that have changed from the last master backup. When you need to restore your data, restore the master backup and the last incremental backup. BackupEDGE can perform different types of incremental backups. Refer to the BackupEDGE manual for the explanation of incremental backups can be performed from the edgemenu utility.

To perform a master backup follow these steps:

+   1. Start the edgemenu program by executing the following command:
edgemenu
nYou will see a window similar to Figure 192 on page 195.
2. Select Backup > Master Backup, and you will see a window similar to Figure 201.

200 Linux System Administration and Backup for IBM @xSeries and Netfinity