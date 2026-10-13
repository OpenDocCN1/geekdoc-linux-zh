can obtain a list of mounted file systems by starting at `rootvfs` and following the `vfs -> vfs_next` chain, as shown in Figure 13.4.

![](bbox=[0.165, 0.1567, 0.9019, 0.5858])

# Figure 13.4 *The Mounted `vfs` List*

The file system framework provides functions, described in Table 13-7, for searching, adding, and removing file systems from the mounted file system list.

# Table 13-7 *Solaris 7 `vfs` Support Functions*

| Method | Description |
|---|---|
| `vfs_add()` | Called by a file system mount function to mount over an existing mount point. For example, the `vfs_mountroot()` method uses this call to mount and unmount root. |
| `vfs_remove()` | Removes a `vfs` object from the chain. Usually called only when unmounting a root overlay. |
| `vfs_lock()` | Locks the entire file system. |
| `vfs_unlock()` | Unlocks the entire file system. |