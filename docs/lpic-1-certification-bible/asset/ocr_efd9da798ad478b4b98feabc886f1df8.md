The bzip2 utility uses the same syntax as the other compression utilities. The correct syntax is as follows:

```
bzip2 -options FILENAME
```

# Managing Quotas

# **2.4 Devices, Linux File Systems, Filesystem Hierarchy Standard**

+   *   **Set and view disk quota.** Setup disk quota for a filesystem, edit user quota, check user quota, generate reports of user quota. Includes quota, edquota, repquota, quotaon, quotaon commands.

Another part of managing files and directories on a Linux system involves working with *quotas*. Users can quickly fill system drives, and it seems that regardless of the amount of disk space installed on a system, that space is never enough. To prevent the users on your system from using all of the available space to store personal files, including large image and music files, you can use disk quotas. Quotas place a limit on the amount of disk space any single user can use. If the user reaches the quota, he or she is unable to create new files.

Linux includes several tools for managing quotas. The *quota, edquota, repquota*, and *quotaon* utilities work together to provide a total quota solution. Each of these utilities is covered in the sections below.

# quota

The *quota* utility is used to view information about disk usage and user quotas. Users are able to view information only for their own user account and groups, but the superuser can view this information for all users and groups. Quota information can be displayed for all file systems listed in `/etc/fstab`; this file contains information regarding whether quotas can be used on the various file systems. The files used to manage quotas are located in file system root and are *quota.user* for user accounts and *quota.group* for group quotas. These files must be created by the superuser and must be created with read and write permissions only for the superuser account. These files are not manually edited when working with quotas. Instead, the tools covered in the following sections are utilized when managing quotas. Quotas are specified at the partition level, which enables you to control which partitions use quotas and to set these quotas independently.

Understanding the relationship between user and group quotas is important. User and group quotas are set individually. When a user creates a new file, that user's account and group both have ownership of the file. If a user's group has exceeded