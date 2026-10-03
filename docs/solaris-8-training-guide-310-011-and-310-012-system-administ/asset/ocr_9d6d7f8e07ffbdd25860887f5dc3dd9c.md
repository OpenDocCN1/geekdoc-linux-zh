<cluster_name> must be in the form SUNWCname. To view detailed information about clusters and their names, start AdminTool on an installed system and choose Browse, Software.

# dontuse

dontuse designates one or more disks that you don’t want the Solaris installation program to use. By default, the installation program uses all the operational disks on the system. <disk_name> must be specified in the form c?t?d? or c’d?, such as c0t0d0.

Here’s the syntax:

```
dontuse disk_name [disk_name...]
```

Here’s an example:

```
dontuse c0t0d0 c0t1d0
```

> NOTE You cannot specify the usedisk keyword and the dontuse keyword in the same class file.

# filesys

filesys sets up the installed system to mount remote file systems automatically when it starts up. You can specify filesys more than once. The following syntax describes using filesys to set up mounts to remote systems:

```
filesys <server>:<path> <server_address> <mount_pt_name> \
[mount_options]
```

The filesys keywords are described in Table 21.8.

# TABLE 21.8

# FILESYS KEYWORDS

| Keyword | Description |
|---|---|
| `<server>:` | The name of the server where the remote file system resides. Don’t forget to include the colon (:). |
| `<path>` | The remote file system’s mount point name. |
| `<server_address>` | The IP address of the server specified in `<server>:<path>`. If you don’t have a name service running on the network, this value can be used to populate the /etc/hosts file with the server’s IP address, but you must specify a minus sign (-). |