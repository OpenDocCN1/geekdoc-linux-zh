read permission, while allowing user and group read access, which results in permissions of rwXr-x---:

```
`$ umask -S u=rwx,g=rx,o=`
```

When you use the binary format, the mask is the inverse of the permissions you want to set. So to set both the read and execute permission on and the write permission off, you would use the octal number 2, a binary 010. To set all permissions on, you would use an octal 0, a binary 000. The following example shows the mask for the permission defaults rwx, rx, and rx (rw, r, and r for files):

```
```
$ umask
0022
```
```

To set the default to only deny all permissions for others, you would use 0027, using the binary mask 0111 for the other permissions.

```
`$ umask 0027`
```

# ## Disk Quotas

You can use disk quotas to control how much disk space a particular user makes use of on your system. On your Linux system, unused disk space is held as a common resource that each user can access as he or she needs it. As users create more files, they take the space they need from the pool of available disk space. In this sense, all the users are sharing a single resource of unused disk space. However, if one user were to use up all the remaining disk space, none of the other users would be able to create files or even run programs. To counter this problem, you can create disk quotas on particular users, limiting the amount of available disk space they can use.

# ### Quota Tools

Quota checks can be implemented on the file system of a hard disk partition mounted on your system. The quotas are enabled using the **quotacheck** and **quotaon** programs. They are executed in the */etc/rc.d/rc.sysinit* script, which is run whenever you start up your system. Each partition needs to be mounted with the quota options, **usrquota** or **grpquota**. **usrquota** enables quota controls for users, and **grpquota** works for groups. These options are usually placed in the mount entry in the */etc/fstab* file for a particular partition (see Chapter 30). For example, to mount the */dev/hda6* hard disk partition mounted to the */home* directory with support for user and group quotas, you would require a mount entry like the following:

```
`/dev/hda6 /home ext2 defaults,usrquota,grpquota 1 1`
```

You also need to create **quota.user** and **quota.group** files for each partition for which you enable quotas. These are the quota databases used to hold the quota information for each user and group. You can create these files by running the **quotacheck** command with the **-a** option or the device name of the file system where you want to enable quotas. The following example creates the quota database on the hda1 hard disk partition:

```
`quotacheck -a /dev/hda1`
```