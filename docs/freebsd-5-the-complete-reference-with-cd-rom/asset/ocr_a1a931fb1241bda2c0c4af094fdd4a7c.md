+   ///user@server/share  This required option specifies the username to be used to access the share (user), the NetBIOS name of the server (server), and the share name on the server (share).

+   /mount/point  This option is the local mount point to be used to hold the share's files.

As an example, consider the following command:

```
# mount_smbfs -u 65534 -f 0444 -d 0555 //sjones@smbsrv/images &gt; /usr/local/graphics
```

This command mounts the images share from smbsrv, using the sjones account, to /usr/local/graphics. Files will be owned by nobody (who has UID 65534) and be readable to all users (0444 permissions on files and 0555 on directories), but writable to none.

After you issue the mount_smbfs command, you'll be asked for a password, unless you include the -N option. To use this option, you need a /usr/local/etc/nsmb.conf file or a ~/.nsmbrc file in the home directory of the user who runs mount_smbfs (normally root). This file contains information in groups according to the server. The basic information for mounting the share without a password takes the following form:

```
{servername:username:sharename} 
password=pass
```

You can add other options, as well. For instance a workgroup=wgnme line sets the workgroup, so you can omit the -w command-line option. You can set the IP address of the server with the addr=ip-address option.

> Caution: If you store passwords in the nsmb.conf or .nsmbrc file, those passwords are potentially accessible to others. Be sure to set 0600 permissions on the file to prevent others from reading it. In the case of nsmb.conf, the file should be owned by root; for .nsmbrc, by the user who runs the mount_smbfs command.

Ordinarily, only root may use mount_smbfs. If you want to give ordinary users the ability to mount SMB/CIFS shares, you can make the mount_smbfs program SUID root, as described in Chapter 8:

```
# chmod a+s /sbin/mount_smbfs
```