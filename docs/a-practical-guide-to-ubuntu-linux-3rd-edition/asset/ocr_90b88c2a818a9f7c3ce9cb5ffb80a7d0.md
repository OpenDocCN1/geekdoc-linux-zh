| `no_all_squash` (all_squash) | Does not change the mapping of users making requests of the NFS server. The all_squash option maps requests from all users—not just root—on remote systems to appear to come from the UID 65534, a nonprivileged user on the local system, or as specified by anounid. This option is useful for controlling access to exported public FTP, news, and other directories. |

| `anounid=un and anongid=gn` | Set the UID or the GID of the anonymous account to un or gn, respectively. NFS uses these accounts when it does not recognize an incoming UID or GID and when it is instructed to do so by root_squash or all_squash. |

# WHERE THE SYSTEM KEEPS NFS MOUNT INFORMATION

A server holds several lists of directory hierarchies it can export. The list that you as a system administrator work with is/etc/exports. The following discussion assumes that the local server,plum, is exporting these directory hierarchies:

```
$ cat /etc/exports

/home grape(rw,no_subtree_check)

/ p16 192.168.0.12(rw,no_subtree_check) jam(rw,no_subtree_check)
```

As explained in more detail on page 791, exports displays the list of exported directory hierarchies:

```
$ exportfs

/home grape

/ p16 jam

192.168.0.12
```

The important files and pseudofiles that NFS works with are described next.

/var/lib/nfs/etab (export table) On the server, lists the directory hierarchies that are exported (can be mounted, but are not necessarily mounted at the moment) and the options they are exported with:

```
$ cat /var/lib/nfs/etab

/home grape(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anounid=65534,anongid=65534)

/ p16 jam(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anounid=65534,anongid=65534)

/ p16 192.168.0.12(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anounid=65534,anongid=65534)
```

The preceding output shows that grape can mount/home and that jam and 192.168.0.12 can mount/p16. The etab file is initialized from/etc/exports when the system is brought up, read by mounted when a client asks to mount a directory hierarchy, and modified by exports (page 791) as the list of exported directory hierarchies changes.