
It wouldn’t make sense to assign values to used and to the other size properties, so these properties are read-only. If the specific rules for calculating used don’t meet your needs, other properties such as usedbychildren and usedbysnapshots may give you better insight into how your disk space is being consumed. See the ZFS admin guide for a complete list.

You can set additional, nonstandard properties on filesystems for your own use and for the use of your local scripts. The process is the same as for standard properties. The names of custom properties must include a colon to distinguish them from standard properties.

## One filesystem per user

Since filesystems consume no space and take no time to create, the optimal number of them is closer to “a lot” than “a few.” If you keep users’ home directories on a ZFS storage pool, it’s recommended that you make each home directory a separate filesystem. There are several reasons for this convention.

- If you need to set disk usage quotas, home directories are a natural granularity at which to do this. You can set quotas on both individual users’ filesystems and on the filesystem that contains all users.

- Snapshots are per filesystem. If each user’s home directory is a separate filesystem, the user can access old snapshots through ~/.zfs.²³ This alone is a huge time saver for administrators because it means that users can service most of their own file restore needs.

- ZFS lets you delegate permission to perform various operations such as taking snapshots and rolling back the filesystem to an earlier state. If you wish, you can give users control over these operations for their own home directories. We do not describe the details of ZFS permission management in this book; see the ZFS Administration Guide.

## Snapshots and clones

ZFS is organized around the principle of copy-on-write. Instead of overwriting disk blocks in place, ZFS allocates new blocks and updates pointers. This approach makes ZFS resistant to corruption because operations can never end up half-completed in the event of a power failure or crash. Either the root block is updated or it’s not; the filesystem is consistent either way (though a few recent changes may be “undone”).

Just as in a logical volume manager, ZFS brings copy-on-write to the user level by allowing you to create instantaneous snapshots. However, there’s an important difference: ZFS snapshots are implemented per-filesystem rather than per-volume, so they have arbitrary granularity. Solaris uses this feature to great effect in the Time Slider widget for the GNOME desktop. Much like Mac OS’s Time Machine, the Time Slider is a combination of scheduled tasks that create and manage snapshots at regular intervals and a UI that makes it easy for you to reach older versions of your files.

On the command line, you create snapshots with zfs snapshot. For example, the following command sequence illustrates creation of a snapshot, use of the snapshot through the filesystem’s .zfs/snapshot directory, and reversion of the filesystem to its previous state.

```
solaris$ sudo touch /opt/demo/new_fs/now_you_see_me
solaris$ ls /opt/demo/new_fs
now_you_see_me
solaris$ sudo zfs snapshot demo/new_fs@snap1
solaris$ sudo rm /opt/demo/new_fs/now_you_see_me
solaris$ ls /opt/demo/new_fs
solaris$ ls /opt/demo/new_fs/.zfs/snapshot/snap1
now_you_see_me
solaris$ sudo zfs rollback demo/new_fs@snap1
solaris$ ls /opt/demo/new_fs
now_you_see_me
```

You assign a name to each snapshot at the time it’s created. The complete specifier for a snapshot is usually written in the form filesystem@snapshot.

Use zfs snapshot -r to create snapshots recursively. The effect is the same as executing zfs snapshot on each contained object individually: each subcomponent receives its own snapshot. All the snapshots have the same name, but they’re logically distinct.

ZFS snapshots are read-only, and although they can bear properties, they are not true filesystems. However, you can instantiate a snapshot as a full-fledged, writable filesystem by "cloning" it.

```
solaris$ sudo zfs clone demo/new_fs@snap1 demo/subclone
solaris$ ls /opt/demo/subclone
now_you_see_me
solaris$ sudo touch /opt/demo/subclone/and_me_too
solaris$ ls /opt/demo/subclone
and_me_too    now_you_see_me
```

The snapshot that is the basis of the clone remains undisturbed and read-only. However, the new filesystem (demo/subclone in this example) retains a link to both the snapshot and the filesystem on which it’s based, and neither of those entities can be deleted as long as the clone exists.

Cloning isn’t a common operation, but it’s the only way to create a branch in a filesystem’s evolution. The zfs rollback operation demonstrated above can only revert a filesystem to its most recent snapshot, so to use it you must permanently delete (zfs destroy) any snapshots made since the snapshot that is your reversion target. Cloning lets you go back in time without losing access to recent changes.
