# CHAPTER 23 Network File System (NFS) 611

Here is the format of each entry/line in the /etc/exports file:

```
/directory/to/export client|ip_network(permissions) client|ip_network(permissions)
```

The different fields are explained here:

+   - directory/to/export This is the directory you want to share with other users— for example, .home.

+   - client This refers to the hostname(s) of the NFS client.

+   - ip_network This allows the matching of hosts by IP addresses (for example, 172.16.1.1) or network addresses with a netmask combination (for example, 172.16.0/16). Wildcard characters such as * and ? are also supported in this field.

+   - permissions These are the corresponding permissions for each client. Table 23-1 describes the valid permissions for each client.

| Permission Option | Meaning |
| --- | --- |
| secure | The port number from which the client requests a mount must be lower than 1024. This permission is on default. To turn it off, specify insecure instead. |
| ro | Allows read-only access to the partition. This is the default permission whenever nothing is specified explicitly. |
| rw | Allows normal read/write access. |
| noaccess | The client will be denied access to all directories below /dir/to/mount. This allows you to export the directory /dir to the client and then specify /dir/to as inaccessible without taking away access to something like /dir/from. |
| root_squash | This permission prevents root users from using superuser (root) privileges on remote NFS-mounted volumes. squash literally means to squash the power of the root user. |
| no_root_squash | This allows the root user on the client host to access the NFS-mounted directory with the same rights and privileges that the superuser would normally have. |
| all_squash | Maps all user IDs (UIDs) and group IDs (GIDs) to the anonymous user. The opposite option is no_all_squash, which is the default setting. |

Table 23-1 NFS Permissions