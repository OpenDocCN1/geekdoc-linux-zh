# 778 CHAPTER 22 NFS: SHARING FILESYSTEMS

prevents character and block special files (page 504) on the mounted hierarchy from being used as devices.
stab file If you mount directory hierarchies frequently, you can add entries for the directory hierarchies to the /etc/fstab file (page 781). (Alternatively, you can use automount; see page 792.) The following /etc/fstab entries automatically mount the same directory hierarchies as in the previous example at the same time that the system mounts the local files:

```
$ cat /etc/fstab
dog:/home /dog.home nfs rw 0 0
dog:/export/progs /apps nfs ro,nosuid 0 0
dog:/export/oracle /oracle nfs ro 0 0
```

A file mounted using NFS is always of type nfs on the local system, regardless of what it is on. Typically you do not run fck or back up an NFS directory hierarchy. The entries in the third, fifth, and sixth columns of fstab are usually nfs (filesystem type), 0 (do not back up this directory dump [page 603]), and 0 (do not run fck [page 512]) on this directory hierarchy.
The options for mounting an NFS directory differ from mount-the data stored in an ext4 or other type of filesystem. See the section on mount (below) for details.

Unmounting directory hierarchies Use to mount a remote directory hierarchy the same way you mount a local filesystem (page 509).

# mount: Mounts A DIRECTORY HIERARCHY

The mount utility (page 506) associates a directory hierarchy with a mount point (directory). You can use mount to mount an NFS (remote) directory hierarchy. This section describes some mount options. It lists default options first, followed by non-default options (enclosed in parentheses). You can use these options on the command line or set in /etc/fstab (page 781). For a complete list of options, refer to the mount and nfs pages.

# ATTRIBUTE CACHING

A file inode (page 501) stores file attributes that provide information about a file, such as file modification time, size, links, and owner. File attributes do not include the data stored in a file. Typically file attributes do not change often for an ordinary file; they change even less for a directory file. The size attribute does not change with every write instruction: When a client is writing to an NFS-mounted file, before the data is transferred to the server. In addition, many file accesses, such as performed by ls, are read-only operations and, therefore, do not change the file's attributes or contents. Thus a client can cache attributes and avoid costly network reads.

The kernel uses the modification time of the file to determine when its cache is out-of-date. If the time the attribute cache was saved is later than the modification time of the file itself, the data in the cache is current. The server must periodically refresh