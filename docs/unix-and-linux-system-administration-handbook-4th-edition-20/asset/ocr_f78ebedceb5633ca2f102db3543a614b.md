# Chapter 30 Cooperating with Windows

; DFS symlinks in the directory of this share.
msdfs root = yes
path = /home/dfs/mydfs

You create symbolic links in /home/dfs/mydfs to set up the actual automounts. For example, the following command makes the jump "directory" a link to one of two directories on other servers. (Note the quite notes. They are required for protection of the backslashes).

```
$ sudo ln -s 'msdfs:serverX/shareX,serverY/shareY' jump
```

If more than one source is provided (as here), Windows will fail over between users. Who use as\myddfs\jump on serverX or serverY, depending on availability. If the filesystems are exported read/write, make sure you use some mechanism in place to synchronize the files. rsync can be helpful for this.

With Samba, you can also redirect all clients that have a particular share to a different server. This is something a Windows server cannot.

```
[myredirect]
msdfs root = yes
msdfs proxy = \serverZ\shareZ
```

Note that DFS only works for users who have the same username and password on all the servers.

# smbclient: a simple CIFS client

In addition to its many server-side features, the Samba package includes a simple command-line file transfer program smbclient. You can use this program to access any Windows or Samba server. For example:

```
$ smbclient=[php/c/$ -U BOULDER]@ben
Password:password
Domain=[BOULDER] OS=[Windows Vista (TM) Business 6001 Service Pack 1
Server=[Windows Vista (TM) Business 6.0]
smb: \_
```

Once you have successfully logged in to the file server, you can use ftp-type commands (as get, put, lcd, and dir) to navigate and transfer files. Type ? to see a full list of the available commands.

# Linux client-side support for CIFS

Linux includes direct client-side support for the SMB/CIFS filesystem. You can mount a CIFS share into your filesystem tree much as you can with any other filesystem that is directly understood by the kernel. For example:

```
$ sudo mount -t cifs -o username=joe /redmond/home/joe/mnt
```

Although this feature is useful, keep in mind that Windows conceptualizes net-work mounts as being established by a particular user (hence the username=joe

![](bbox=[0.196, 0.8, 0.243, 0.838])