If you want to change your `umask` value, issue the `umask` command followed by the permission level you want to define. So, if you want the permissions to be `rw-r----` on files and `rwxr-x---` on directories, enter the following:

```
```bash
umask 027
```
```

This will temporarily change your mask. After you log off and log on again, the prior setting will return. To make this change permanent, add the previous command to your startup file. Only root can change the system `umask` value. See Chapter 7 for more information on using your startup files to manage your environment.

# ## Summary

Permissions are an essential part of managing your system. They enable you to control who gets to access what. The possible permissions are read, write, and execute. For the exam, you need to understand what each permission allows the user to do whether applied to a file or a directory.

The permission block is the first 10 characters that are displayed when issuing the `ls -1` command. The first character designates the file type; the next three are the permissions for the owner; the next three after that are the permissions for the group; and the last three are the permissions for user. These permissions are then applied to one of three entities: owner, group, or user. You can change these permissions through the use of the `chmod` command. Permissions can be changed using either symbols or numbers.

To change the owner of a file or directory, use the `chown` command. Use either `chown` or `chgrp` to change the group associated with a file. The set UID (SUID) and set GID (SGID) are two special permissions that also can be applied. SUID allows an executable to be executed with another user's permissions instead of those of the user running the executable. The SGID works the same way, except it allows the permissions of another group rather than another user.

Another special permission is the sticky bit. This assists in the management of world-write directories. It also can be used to improve application execution. In addition, you need to understand what the `umask` is and how to correctly set it. Default permissions for all newly created files are defined by the system `umask` value. A user-specific `umask` also can be defined.