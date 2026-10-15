```
zfs set sharenfs=off data01
```

This file system persists after reboot!

# 8. How to take snapshots of file systems:

Taking a "snapshot" of a file system is like taking a picture: changes are recorded to the snapshot when the original file system changes; to remove a dataset all previous snapshots have to be removed. You can also rename snapshots. You cannot destroy a snapshot if it has a clone.

```
zfs snapshot data01@10022010
```

Creates a snapshot.

Further examples:

```
zfs snapshot data01@10022010 data01@mybackup
```

Renames a snapshot.

```
zfs destroy data01@10022010
```

Destroys a snapshot.

# 9. How to roll back a file system:

By default, you can only roll back to the latest snapshot. To roll back to older ones, you must delete all newer snapshots.

```
zfs rollback data01@10022010
```

# 10. Cloning/promoting file systems:

Clones are writable file systems that have been upgraded from a snapshot. A dependency will remain on the snapshot as long as the clone exists. A clone uses the data from the snapshot to exist. As you use the clone, it uses space separate from the snapshot. Clones cannot be created across zpools, you need to use the zfs send/receive commands to do this, as shown in Example 24.4.

```
zfs clone data7@10022010 data8/clone
```

```
zfs clone -o mountpoint=/clone data7@10022010 data8/clone
```

Clones, changes the mount point of the clone.

Further examples:

```
zfs promote data8/clone
```

Promotes a clone. This allows you to destroy the original file system that the clone is attached to. The clone must reside in the same pool!

# 11. Renaming a file system:

```
zfs rename data03/koretksy_disk01 data03/koretksy_d01
```

The dataset must be kept within the same pool. There are two options on this command: -p creates all the nonexistent parent datasets; -r recursively rename the snapshots of all descendant datasets (used with snapshots only).