# Table 18.8 How to specify the number of nfsd daemons

| System | Config file (in /etc) | Option to set | Default |
| Ubuntu | default/nfs-kernel-server | RPCNFSDCOUNT | 8 |
| SUSE | sysconfig/nfs | USE_KERNEL_NFSD_NUMBER | 4 |
| Red Hat | sysconfig/nfs | RPCNFSDCOUNT | 8 |
| Solaris | default/nfs | NFSD_SERVERS | 16 |
| HP-UX | default/nfs | NFSD_SERVERS | 16 |
| AIX | Use SMIT or chnfs to change the number of nfsd daemons. | | |

# 18.4 CLIENT-SIDE NFS

NFS filesystems are mounted in much the same way as local disk filesystems. The mount command understands the notation hostname:directory to mean the path directory on the host hostname. As with local filesystems, mount maps the remote directory on the remote host into a directory within the local file tree. After the mount completes, you access an NFS-mounted filesystem just like a local filesystem. The mount command and its associated NFS extensions represent the most significant concerns to the system administrator of an NFS client.

Before an NFS file system can be mounted, it must be properly exported (see Server-side NFS on page 698). To verify that a server has properly exported its filesystems from the client's perspective, use the client's showmount command:

```
$ showmount -e monk
Export list for monk:
/home/ben harp.atrust.com
```

This example reports that the directory /home/ben on the server monk has been exported to the client system harp.atrust.com. If an NFS mount is not working, first verify that the filesystems have been properly exported on the server with exports. (You might have just forgotten to run exports -a after updating the exports file.) Next, check the showmount output.

If the directory is properly exported on the server but showmount returns an error or an empty list, you might double-check that all the necessary processes are running on the server (portmap, mountd, nfsd, statd, and lockd), that the hosts.allow and hosts.deny files allow access to those daemons, and that you are on the right client system.

The path information displayed by showmount, such as /home/ben above, is only valid for NFS version 2 and 3 servers. NFS version 4 servers export a single unified pseudo-filesystem. The traditional NFS concept of separate mount points doesn't jive with version 4's model, so showmount isn't applicable.

Unfortunately, there is no good replacement for showmount in NFSv4. On the server, the command exportfs -v shows the existing exports, but of course this only works locally. If you don't have direct access to the server, mount the root of

See page 917 for more information about hosts.* files and TCP wrappers.