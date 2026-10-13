# Disk Quotas

You can use disk quotas to control how much disk space a particular user makes use of on your system. On your Linux system, unused disk space is held as a common resource that each user can access as they need it. As a user creates more files, they take the space they need from the pool of available disk space. In this sense, all the users are sharing a single resource of unused disk space. However, if one user were to use up all the remaining disk space, none of the other users would be able to create files or even run programs. To counter this problem, you can create disk quotas on particular users, limiting the amount of available disk space they can use.

# Quota Tools

Quota checks can be implemented on the file system of a hard disk partition mounted on your system. The quotas are enabled using the quotacheck and quotaon programs. On Red Hat, they are executed in the /etc/rc.d/rc.sysinit script, which is run whenever you start up your system. Each partition needs to be mounted with the quota options, usrquota or grpquota. usrquota enables quota controls for users, and grpquota works for groups. These options are usually placed in the mount entry in the /etc/fstab file for a particular partition (see Chapter 30). For example, to mount the /dev/hda6 hard disk partition mounted to the /home directory with support for user and group quotas, you would require a mount entry like the following:

```
/dev/hda6 /home ext2 defaults,usrquota,grpquota 1 1
```

You also need to create quota.user and quota.group files for each partition for which you enable quotas. These are the quota databases used to hold the quota information for each user and group. You can create these files by running the quotacheck command with the -a option or the device name of the file system where you want to enable quotas. The following example creates the quota database on the hda1 hard disk partition.

```
quotacheck -a /dev/hda1
```

# edquota

You can set disk quotas using the edquota command. With it, you can access the quota record for a particular user and group, which is maintained in the disk quota database. You can also set default quotas that will be applied to any user or group on the file system for which quotas have not been set. edquota will open the record in your default editor, and you can use your editor to make any changes. To open the record for a particular user, use the -u option and the username as an argument for edquota (see Table 28-5). The following example opens the disk quota record for the user larisa:

```
edquota -u larisa
```

The limit you set for a quota can be hard or soft. A hard limit will deny a user the ability to exceed their quota, whereas a soft limit will just issue a warning. For the soft limit, you can designate a grace period during which time the user has the chance to reduce their disk space below the limit. If the disk space still exceeds the limit after the grace period expires, the user can be denied access to their account. For example, a soft limit is typically 75 megabytes, whereas the hard limit could be 100 megabytes. Users who exceed their soft limit could have a 48-hour grace period.

The quota record begins with the hard disk device name and the blocks of memory and inodes in use. The Limits segments have parameters for soft and hard limits. If these entries are 0, there are no limits in place. You can set both hard and soft limits, using the hard limit as a firm restriction. Blocks in Linux are currently about 1,000 bytes. The inodes are used by files to hold information about the memory blocks making up a file. To set the time limit for a soft limit, use the edquota command with the -t option. The following example displays the quota record for larisa:

```
Quotas for user larisa:
/dev/hda3: blocks in use: 9000, limits (soft = 40000, hard = 60000)
inodes in use: 321, limits (soft = 0, hard = 0)
```