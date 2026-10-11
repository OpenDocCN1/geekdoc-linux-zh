The /etc/exports file lists all directories to be shared out by the NFS server. Each line in the file lists a directory to be exported, along with options that apply to that export. A directory can only be exported once. The following is a sample /etc/exports file:

```
/pub                     (r)       *.the-nashes.net(rw)
/home                     192.168.0.0/24(rw)
/documents         norbert(ro,root_squash)
```

On the left is the directory to be exported; on the right are the systems allowed to connect and any permission options applied to them. Wildcard domain names can be used. When a client connects, their IP address is reversed to their hostname and checked against the /etc/exports file. Table 16-18 lists the permissions options available.

| Option | Function |
| :--- | :--- |
| ro | Export the directory with read-only access. |
| rw | Export the directory with read and write access (depending on the user's permissions). |
| rw=<list> | Export the directory with read-only access, except for those hosts listed. |
| root_squash | Remap the root user (UID 0 and GUID 0) to that of the user nobody or the user specified by anonuid and the group specified in anongid. This is the default. |
| no_root_squash | Do not remap root user access. |
| all_squash | Remap all users to user nobody. |
| anonuid=<uid> | The user number that root is mapped to with root_squash. |
| anonguid=<guid> | The group number that root is mapped to with root_squash. |
| secure | Require that the client's originating port be 1023 or less. |
| insecure | Allow any originating port on the client. |
| sync | Require that all write requests be committed to disk before being completed. |

When a change is made to /etc/exports, the exportfs command needs to be used to update the server. Table 16-19 lists the options for exportfs. The exportfs tool can also be used to add and remove individual exports without