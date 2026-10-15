```
zfs list -o poolname,mounted,sharenfs,mountpoint
```

Complex listing: there are a number of attributes that you can use in a complex listing; see the man page for zfs.

# 2. How to create a file system:

```
zfs create data01/sarwar
```

Presumes a pool called data01, creates a /data01/sarwar ZFS file system.

Further examples:

```
zfs create -o mountpoint=/users/data01/users
```

Creates at a different mount point.

# 3. How to destroy a file system:

```
zfs destroy data01/sarwar
```

Further examples:

```
zfs destroy -r data01/sarwar
```

```
zfs destroy -R data01/sarwar
```

Uses the recursive options -r (all children), -R (all dependents).

# 4. How to mount a file system:

```
zfs mount data01
```

Further examples:

```
zfs mount -o mountpoint=/tmpmnt data01/sarwar
```

You can create temporary mount that expires after unmounting. You can apply all the normal mount options—that is, ro/rw, setuid, and so on.

# 5. How to unmount a file system:

```
zfs umount data01
```

# 6. How to share a file system:

```
zfs share data01
```

Further examples:

```
zfs set sharenfs=on data01
```

This file system persists after reboots!

```
zfs set sharenfs="*rw@192.168.0.13/24" data01/sarwar
```

Shares with specific hosts.

# 7. How to unshare a file system:

```
zfs unshare data01
```

Further examples: