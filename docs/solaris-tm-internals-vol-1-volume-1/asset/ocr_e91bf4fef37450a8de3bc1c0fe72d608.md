# Table 13-1  *Solaris 7 vnode Types from* `sys/vnode.h`  *(Continued)*

| Type | Description |
|---|---|
| `VSOCK` | `sockfs` node (socket) |
| `VBAD` | Bad vnode |

# 13.2.2 Vnode Methods

The vnode interface provides the set of file system object methods, some of which we saw in Figure 13.1 on page 542. The file systems implement these methods to perform all file system-specific file operations. Table 13-2 shows the vnode interface methods in Solaris.

# Table 13-2  *Solaris 7 Vnode Interface Methods from* `sys/vnode.h`

| Method | Description |
|---|---|
| `vop_access()` | Checks access to the supplied vnode. |
| `vop_addmap()` | Increments the map count. |
| `vop_close()` | Closes the file given by the supplied vnode. When this is the last close, some file systems use `vop_close()` to initiate a writeback of outstanding dirty pages by checking the reference count in the vnode. |
| `vop_cmp()` | Compares two vnodes. |
| `vop_create()` | Creates the supplied path name. |
| `vop_delmap()` | Decrements the map count. |
| `vop_dispose()` | Frees the given page from the vnode. |
| `vop_dump()` | Dumps data when the kernel is in a frozen state. |
| `vop_dumpctl()` | Prepares the file system before and after a dump. |
| `vop_frlock()` | Does file and record locking for the supplied vnode. |
| `vop_fsync()` | Flushes out any dirty pages for the supplied vnode. |
| `vop_getattr()` | Gets the attributes for the supplied vnode. |
| `vop_getpage()` | Gets pages in the range offset and length for the vnode from the backing store of the file system. Does the real work of reading a vnode. This method is often called as a result of `read()`, which causes a page fault in `seg_map`, which calls `vop_getpage`. |
| `vop_getsecattr()` | Gets security access control list attributes. |
| `vop_inactive()` | Frees resources and releases the supplied vnode. The file system can choose to destroy the vnode or put it onto an inactive list, which is managed by the file system implementation. |
| `vop_ioctl()` | Performs an I/O control on the supplied vnode. |
| `vop_fid()` | Gets a unique file ID for the supplied vnode. Used for NFS client consistency. |