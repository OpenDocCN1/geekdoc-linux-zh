# MOUNTING SHARES

The mount utility (page 520) with a -t cifs option mounts a share as if it were a Linux directory hierarchy. See page 1242 for more information on the CIFS protocol. When you mount a share, you can write to the files on the share; you cannot write to files on a share using smbclient.

A mount command that mounts a share has the following syntax (you must run this command with root privileges):

```
mount -t cifs //host/share dir
```

where host is the name of the system the share is on, share is the name of the share you want to mount, and dir is the absolute pathname of the Linux directory you are mounting the share on (the mount point).

The following command, when run with root privileges, mounts on the /plum.sam directory the sam share on plum:

```
# mount -t cifs //plum.sam /plum.sam -o username=sam
Password for sam@/plum.sam: ****** RETURN
# ls /plum.sam
Desktop Documents Downloads Music Pictures Public ...
```

Omit the username argument and provide a blank password to mount shares that are visible to an anonymous user.

Use the uid, file_mode, and dir_mode mount options with type cifs filesystems to establish ownership and permissions of mounted files:

```
# mount -t cifs //plum.sam /plum.sam -o username=sam,uid=sam,file_mode=0644,dir_mode=0755
```

Permissions must be expressed as octal numbers preceded by a zero. For more information refer to the mount.cifs man page.

You can also store the username, password, and optionally the workgroup (domain) in a credentials file. To prevent another user from mounting this share, a credentials file should be owned by root and readable and writable only by a user working with root privileges (600 permissions). When you specify the credentials file in fstab (page 524), the share can be mounted automatically when the system is booted. Following is the credentials file for the share in the preceding example:

```
# cat /etc/plum.sam.credentials
username=sam
password=password
domain=MC5
# ls -l /etc/plum.sam.credentials
-rw------- 1 root root 40 06-27 17:38 /etc/plum.sam.credentials
```