Because Linux directories do not shrink automatically, removing a file from a directory does not shrink the directory, even though it frees up space on the disk. To remove unused space and make a directory smaller, you must copy or move all the files to a new directory *and* remove the original directory.

The following procedure removes unused directory space. First remove all unneeded files from the large directory. Then create a new, empty directory. Next move or copy all remaining files from the old large directory to the new empty directory. Remember to copy hidden files. Finally delete the old directory and rename the new directory.

```
$ sudo mkdir /home/max/new
$ sudo mv /home/max/large/* /home/max/large/.[A-z]*/home/max/new
$ sudo rmdir /home/max/large
$ sudo mv /home/max/new /home/max/large
```

# DISK QUOTA SYSTEM

The disk quota system (supplied by the *quota* software package) limits the disk space and number of files owned by individual users. You can choose to limit each user's disk space, the number of files each user can own, or both. Each resource that is limited has two limits: a lower limit and an upper limit. The user can exceed the lower limit, or *quota*, although a warning is given each time the user logs in when he is above the quota. After a certain number of warnings (set by the system administrator), the system behaves as if the user had reached the upper limit. Once the upper limit is reached or the user has received the specified number of warnings, the user will not be allowed to create any more files or use any more disk space. The user's only recourse at that point is to remove some files.

Users can review their usage and limits with the *quota* utility. Using sudo, you can use *quota* to obtain information about any user. You can turn on quotas only if the filesystem is mounted with the *usrquota* and/or *grpquota* options (ext3 and ext4 filesystems).

First you must decide which filesystems to limit and how to allocate space among users. Typically only filesystems that contain users' home directories, such as /home, are limited. Use the *edquota* utility to set the quotas, and then use *quotaon* to start the quota system. Unmounting a filesystem automatically disables the quota system for that filesystem.

# rsyslogd: LOGS SYSTEM MESSAGES

Traditionally UNIX programs sent log messages to standard error. If a more permanent log was required, the output was redirected to a file. Because of the limitations of this approach, 4.3BSD introduced the system log daemon (rsyslogd) now used by Linux. This daemon listens for log messages and stores them in the