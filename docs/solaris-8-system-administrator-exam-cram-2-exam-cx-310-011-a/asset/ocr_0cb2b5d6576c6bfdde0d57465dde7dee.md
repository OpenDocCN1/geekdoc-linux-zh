| Field | Description |
|---|---|
| Mount Point | Specifies the subdirectory where the NFS resource should be mounted |
| FS Type | Uses nfs to indicate an NFS resource |
| fsck Pass | Uses a hyphen (-) to indicate no entry |
| Mount At Boot | Uses yes to indicate that the resource should be mounted at boot or when the mountall command is executed; otherwise, no |
| Mount Options | Specifies any desired NFS mount options; see Table 18.3 or the manual page for the mount command |

NFS supports *client-side failover*. That is, if an NFS resource becomes unavailable, the client can switch to another NFS server that provides a “replicated” copy of the resource. You enable this failover capability by adding an entry in the /etc/vfstab file for the resource. In the **Device To Mount** field, list the systems that provide the replicated resource, separated by commas. You should also specify the read-only option (**-o ro**) in the **Mount Options** field. For example, to provide client-side failover for the /export/local resource that is available from the **alpha** or the **beta** NFS server and mounted at /usr/local, add the following entry to the /etc/vfstab file:

```
alpha,beta:/export/local - /usr/local nfs - no -o ro
```

![](bbox=[0.1229, 0.561, 0.2176, 0.6308])

The read-only resources (-o ro mount option) should be configured for client-side failover. Also be certain that the system hostnames or IP addresses are valid and separated by commas.

# The mountall and umountall Commands

The **mountall** command is used to mount one or more local file systems and/or remote (NFS) shared file systems or directories. If the name of a file (containing information on one or more resources) is not specified as a command-line argument, the /etc/vfstab is used by default. The **mountall** command will mount only the resources in the file system table (or specified file) that have the **Mount At Boot** column set to **yes**.

If a file system type is specified by using the **-F** command-line option, only file systems of that type are mounted. If the **-l** command-line argument is specified, only local file systems or directories are mounted. If the **-r** command-line argument is specified, only remote shared file systems or directories are mounted.