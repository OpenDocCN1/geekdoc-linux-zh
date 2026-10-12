After you install the NFS client package, you are ready to configure the clients.

# # Configuring an NFS Client

This section assumes that you are configuring Red Hat Linux-based NFS clients. If you are configuring an NFS client on a different platform, read the proper documentation if you need any help. The NFS client package comes with a program called showmount that gives you information on exported file systems or directories on an NFS server. You can run this command with the NFS server's host name or IP address as the argument to see what hosts are allowed to access the exported file systems or directories. For example,

```
showmount  nfs-server.nitec.com
```

shows the list of NFS clients that are allowed to import files from `nfs-server.nitec.com`. To see the NFS server's export list, run this command with the `-e` option. To see which client is allowed to import what file systems or directories, run the command with the `-a` option.

If the showmount command indicates that the NFS client you are configuring is allowed to import a file system or directory, you are ready to continue with client configuration. If it does not show the host name or IP address of your current NFS client, you must reconfigure the `/etc/exports` file on the NFS server to allow this client access to whatever directory or file system you want to import.

To import a directory or file system from an NFS server, you need to mount it using the standard mount command. For example, to mount a directory called `/www` from an NFS server called `nfs-server.nitec.com`, use the following mount command:

```
mount nfs-server.nitec.com:/www /www -t nfs
```

This command mounts the `/www` directory from the `nfs-server.nitec.com` system as an NFS file system that is specified using the `-t` option. However, if you plan to mount an NFS file system or directory on a regular basis and on boot, you have to add a new line in the