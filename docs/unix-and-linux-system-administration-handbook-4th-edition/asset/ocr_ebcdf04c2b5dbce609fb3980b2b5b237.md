It wouldn’t make sense to assign values to used and to the other size properties, so these properties are read-only. If the specific rules for calculating used don’t meet your needs, other properties such as usedbychildren and usedbysnapshots may give you better insight into how your disk space is being consumed. See the ZFS admin guide for a complete list.

You can set additional, nonstandard properties on filesystems for your own use and for the use of your local scripts. The process is the same as for standard properties. The names of custom properties must include a colon to distinguish them from standard properties.

# One filesystem per user

Since filesystems consume no space and take no time to create, the optimal number of them is closer to “a lot” than “a few.” If you keep users’ home directories on a ZFS storage pool, it’s recommended that you make each home directory a separate filesystem. There are several reasons for this convention.

+   - If you need to set disk usage quotas, home directories are a natural granularity at which to do this. You can set quotas on both individual users’ filesystems and on the filesystem that contains all users.

+   - Snapshots are per filesystem. If each user’s home directory is a separate filesystem, the user can access old snapshots through ~/.zfs.²³ This alone is a huge time saver for administrators because it means that users can service most of their own file restore needs.

+   - ZFS lets you delegate permission to perform various operations such as taking snapshots and rolling back the filesystem to an earlier state. If you wish, you can give users control over these operations for their own home directories. We do not describe the details of ZFS permission management in this book; see the ZFS Administration Guide.

# Snapshots and clones

ZFS is organized around the principle of copy-on-write. Instead of overwriting disk blocks in place, ZFS allocates new blocks and updates pointers. This approach makes ZFS resistant to corruption because operations can never end up half-completed in the event of a power failure or crash. Either the root block is updated or it’s not; the filesystem is consistent either way (though a few recent changes may be “undone”).

Just as in a logical volume manager, ZFS brings copy-on-write to the user level by allowing you to create instantaneous snapshots. However, there’s an important difference: ZFS snapshots are implemented per-filesystem rather than per-volume, so they have arbitrary granularity. Solaris uses this feature to great effect in the Time Slider widget for the GNOME desktop. Much like Mac OS’s Time