Called by the VFS when the last reference to an inode is dropped. Normal Unix filesystems do not define this function, in which case the VFS simply deletes the inode.

+   - `void delete_inode(struct inode *inode)`
+       Deletes the given inode from the disk.

+   - `void put_super(struct super_block *sb)`
+       Called by the VFS on umount to release the given superblock object. The caller must hold the `s_lock` lock.

+   - `void write_super(struct super_block *sb)`
+       Updates the on-disk superblock with the specified superblock. The VFS uses this function to synchronize a modified in-memory superblock with the disk. The caller must hold the `s_lock` lock.

+   - `int sync_fs(struct super_block *sb, int wait)`
+       Synchronizes filesystem metadata with the on-disk filesystem. The `wait` parameter specifies whether the operation is synchronous.

+   - `void write_super_lockfs(struct super_block *sb)`
+       Prevents changes to the filesystem, and then updates the on-disk superblock with the specified superblock. It is currently used by LVM (the LogicalVolume Manager).

+   - `void unlockfs(struct super_block *sb)`
+       Unlocks the filesystem against changes as done by `write_super_lockfs`().

+   - `int statfs(struct super_block *sb, struct statfs *statfs)`
+       Called by the VFS to obtain filesystem statistics. The statistics related to the given filesystem are placed in `statfs`.

+   - `int remount_fs(struct super_block *sb, int *flags, char *data)`
+       Called by the VFS when the filesystem is remounted with new mount options. The caller must hold the `s_lock` lock.

+   - `void clear_inode(struct inode *inode)`
+       Called by the VFS to release the inode and clear any pages containing related data.

+   - `void umount_begin(struct super_block *sb)`
+       Called by the VFS to interrupt a mount operation. It is used by network filesystems, such as NFS.

All these functions are invoked by the VFS, in process context. All except `dirfty_inode()` may all block if needed.

Some of these functions are optional; a specific filesystem can then set its value in the superblock operations structure to NULL. If the associated pointer is NULL, the VFS either calls a generic function or does nothing, depending on the operation.