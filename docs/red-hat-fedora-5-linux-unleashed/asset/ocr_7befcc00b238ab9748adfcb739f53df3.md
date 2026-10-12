+   * quotacheck—Updates the status of quotas (compares new and old tables of disk usage); it is run after fsck
+   * edquota—A very basic quota management command

# Manually Configuring Quotas

Manual configuration of quotas involves changing entries in your system’s file system table, /etc/fstab, to add the usrquota mount option to the desired portion of your file system. As an example in a simple file system, quota management can be enabled like this:

```
LABEL=/    /    ext3    defaults,usrquota    1 1
```

Group-level quotas can also be enabled by using the grpquota option. As the root operator, you must then create a file using our example of creating user quotas) named aquota.user in the designated portion of the file system, like so:

```
# touch /quota.user
```

You should then turn on the use of quotas using the quotaon command:

```
# quotaon -av
```

You can then edit user quotas with the edquota command to set hard and soft limits on file system use. The default system editor vi (vi unless you change your EDITOR environment variable) will be launched when editing a user’s quota.

Any user can find out what her quotas are with

```
$ quota -v
```

> **NOTE**
> 
> There are no graphical tools supported by Fedora that can be used to configure disk quotas. A Quota mini-HOWTO is maintained at http://www.tldp.org/HOWTO/mini/Quota.html.

> **RELATED FEDORA COMMANDS**
> 
> You will use these commands to manage user accounts in Fedora:
> * ac—A user account-statistics command
> * change—Sets or modifies user password expiration policies
> * chfn—Creates or modifies user finger information in /etc/passwd
> * chgrp—Modifies group memberships
> * chmod—Changes file permissions
> * chown—Changes file ownerships
> * chpasswd—Batch command to modify user passwords
> * chsh—Modifies a user’s shell
> * groups—Displays existing group memberships