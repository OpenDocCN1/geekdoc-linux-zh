interface achieves independence by means of a virtual file system (vfs) object. The vfs object represents an encapsulation of a file system's state and a set of methods for each of the file system administrative interfaces. Each file system type provides its own implementation of the object. Figure 13.3 illustrates the vfs object.

![](bbox=[0.223, 0.226, 0.818, 0.583])

# **Figure 13.3** *The vfs Object*

Table 13-5 lists all the vfs interface methods.

# **Table 13-5** *Solaris 7 vfs Interface Methods from sys/vfs.h*

| Method | Description |
|---|---|
| `vfs_mount()` | Mounts a file system on the supplied vnode. |
| `vfs_unmount()` | Unmounts the file system. |
| `vfs_root()` | Finds the root vnode for a file system. |
| `vfs_statvfs()` | Queries statistics on a file system. |
| `vfs_sync()` | Flushes the file system cache. |
| `vfs_vget()` | Finds a vnode that matches a unique file ID. |
| `vfs_mountroot()` | Mounts the file system on the root directory. |
| `vfs_swapvp()` | Not used. |