acquires the password through PAM, and a "session" part, which does the actual mounting. Because this is a session module, this enables an unmount of the file systems when the session closes.

> Tip: Check if you need automatic mounting for all modes to log in. For example, a su from root to a user does not work because a password is not provided.

The lines to add look like this:

```
auth        required        pam_mount.so
```

And:

```
session     optional        pam_mount.so
```

The auth line should go before pam_unix and pam_winbind lines. The session line should go in the session section. Remember to add a use_first_auth argument for the line not having one before adding pam_mount; otherwise, a second password prompt shows for that entry.

The pam_mount module has its own configuration file /etc/security/pam_mount.conf. This file contains such as where the mount and unmount commands are found, debug settings, whether mount points should be created, and which file systems should be mounted for users.

A minimum pam_mount.conf file for mounting SMB shares like Example 9-23.

Example 9-23 Minimum pam_mount.conf

```
debug 1
mkmountpoint 1 require nosuid,nodev
lsof /usr/sbin/lsof
fsck /sbin/fsck
losetup /sbin/losetup
unmount /sbin/losetup -d
smbmount /usr/bin/smbmount
unmount /usr/bin/smbumount
volume * smb31ab26 & /home//&domainshare uid=,dmask=0750 -
```

This enables debugging on pam_mount. Points are created when they are non-existent and the share to be mounted is indicated in the last line.

The asterisk near the beginning of the last line in this example indicates that this security is mounted for every user. The ampersand character (&) in the