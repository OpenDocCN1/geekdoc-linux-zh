> NOTE
Even if you share a file system from the command line by typing the share command, mountd and nfsd still won't run until you make an entry into /etc/dfs/dfstab and run the nfs.server script.

After editing the /etc/dfs/dfstab file, restart the NFS server by either restarting it or by typing this:

```
/etc/init.d/nfs.server start
```

You only need to start the nfs.server script after you make the first entry in the /etc/dfs/dfstab file. This is because at startup, when the system enters run level 3, mountd and nfsd are not started if the /etc/dfs/dfstab file is empty. After you have made an initial entry and have executed the nfs.server script, you can modify /etc/dfs/dfstab without restarting the daemons. You simply execute the shareall command, and any new entries in the /etc/dfs/dfstab file are shared.

After you have at least one entry in the /etc/dfs/dfstab file and after both mountd and nfsd are running, you can share additional file systems by typing the share command directly from the command line. Be aware, however, that if you don't add the entry to the /etc/dfs/dfstab file, the file system is not automatically shared the next time the system is restarted.

The dfshares command displays information about the shared resources available to the host from an NFS server. Here is the syntax for dfshares:

```
dfshares <servername>
```

You can view the shared file systems on a remote NFS server by using the dfshares command as follows:

```
dfshares apollo
```

If no servername is specified, all resources currently being shared on the local host are displayed. Another place to find information on shared resources is in the server's /etc/dfs/sharetab file. This file contains a list of the resources currently being shared.

# NFS Security

With NFS, you need to be concerned about security. When you issue the share command, any system can access the file system through your network. It's a good idea to be more specific about who can mount the file system. The following examples illustrate how to set up a share with restrictions as to which hosts can mount the shared resource:

```
share -F nfs -o ro=apollo:neptune:zeus /data
```