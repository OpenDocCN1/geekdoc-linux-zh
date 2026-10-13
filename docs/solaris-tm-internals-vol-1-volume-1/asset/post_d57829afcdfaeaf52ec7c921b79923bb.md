
**Table 13-1** *Solaris 7 vnode Types from* `sys/vnode.h` *(Continued)*

| Type | Description |
|---|---|
| `VSOCK` | `sockfs` node (socket) |
| `VBAD` | Bad vnode |

### 13.2.2 Vnode Methods

The vnode interface provides the set of file system object methods, some of which we saw in Figure 13.1 on page 542. The file systems implement these methods to perform all file system-specific file operations. Table 13-2 shows the vnode interface methods in Solaris.

**Table 13-2** *Solaris 7 Vnode Interface Methods from* `sys/vnode.h`

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
| `vop_link()` | Creates a hard link to the supplied vnode. |
| `vop_lookup()` | Looks up the path name for the supplied vnode. The `vop_lookup()` does file-name translation for the open, stat system calls. |
| `vop_map()` | Maps a range of pages into an address space by doing the appropriate checks and calling `as_map()`. |
| `vop_mkdir()` | Makes a directory of the given name. |
| `vop_open()` | Opens a file referenced by the supplied vnode. The `open()` system call has already done a `vop_lookup()` on the path name, which returned a vnode pointer and then calls to `vop_open()`. This function typically does very little, since most of the real work was performed by `vop_lookup()`. |
| `vop_pageio()` | Paged I/O support for file system swap files. |
| `vop_pathconf()` | Establishes file system parameters with the `pathconf` system call. |
| `vop_poll()` | File system support for the `poll()` system call. |
| `vop_putpage()` | Writes pages in the range offset and length for the vnode to the backing store of the file system. Does the real work of writing a vnode. |
| `vop_read()` | Reads the range supplied for the given vnode. `vop_read()` typically maps the requested range of a file into kernel memory and then uses `vop_getpage()` to do the real work. |
| `vop_readdir()` | Reads the contents of a directory. |
| `vop_readlink()` | Follows the symlink in the supplied vnode. |
| `vop_realvp()` | Gets the real vnode from the supplied vnode. |
| `vop_remove()` | Removes the file for the supplied vnode. |
| `vop_rename()` | Renames the file to the new name. |
| `vop_rmdir()` | Removes a directory pointed to by the supplied vnode. |
| `vop_rwlock()` | Holds the reader/writer lock for the supplied vnode. This method is called for each vnode, with the `rwflag` set to 0 inside a `read()` system call and the `rwflag` set to 1 inside a `write()` system call. POSIX semantics require only one writer inside `write()` at a time. Some file system implementations have options to ignore the writer lock inside `vop_rwlock()`. |
| `vop_rwunlock()` | Releases the reader/writer lock for the supplied vnode. |
| `vop_seek()` | Seeks within the supplied vnode. |
| `vop_setattr()` | Sets the attributes for the supplied vnode. |
| `vop_setfl()` | Sets file locks on the supplied vnode. |
| `vop_setsecattr()` | Sets security access control list attributes. |
| `vop_shrlock()` | ONC shared lock support. |
| `vop_space()` | Frees space for the supplied vnode. |
| `vop_symlink()` | Creates a symbolic link between the two path names. |
| `vop_write()` | Writes the range supplied for the given vnode. The write system call typically maps the requested range of a file into kernel memory and then uses `vop_putpage()` to do the real work. |

### 13.2.3 vnode Reference Count

A vnode is created by the file system at the time a file is first opened or created and stays active until the file system decides the vnode is no longer needed. The vnode framework provides an infrastructure that keeps track of the number of references to a vnode. The kernel maintains the reference count by means of the `VN_HOLD()` and `VN_RELE()` macros, which increment and decrement the `v_count` field of the vnode. A vnode stays valid while its reference count is greater than zero, so a subsystem can rely on a vnode’s contents staying valid by calling `VN_HOLD()` before it references a vnode’s contents. It is important to distinguish a vnode reference from a lock; a lock ensures exclusive access to the data, and the reference count ensures persistence of the object.

When a vnode’s reference count drops to zero, `VN_RELE()` invokes the `VOP_INACTIVE()` method for that file system. Every subsystem that references a vnode is required to call `VN_HOLD()` at the start of the reference and to call `VN_RELE()` at the end of each reference. Some file systems deconstruct a vnode when its reference count falls to zero; others hold on to the vnode for a while so that if it is required again, it is available in its constructed state. The UFS file system, for example, holds on to the vnode for a while after the last release so that the virtual memory system can keep the inode and cache for a file, whereas the PCFS file system frees the vnode and all of the cache associated with the vnode at the time `VOP_INACTIVE()` is called.

### 13.2.4 Interfaces for Paging vnode Cache

Solaris unifies file and memory management by using a vnode to represent the backing store for virtual memory. A page of memory represents a particular vnode and offset. The file system uses the memory relationship to implement caching for vnodes within a file system. To cache a vnode, the file system has the memory system create a page of physical memory that represents the vnode and offset.

The virtual memory system provides a set of functions for cache management and I/O for vnodes. These functions allow the file systems to cluster pages for I/O and handle the setup and checking required for syncing dirty pages with their backing store. The functions, described in Table 13-3, set up pages so that they can be passed to device driver block I/O handlers.

**Table 13-3** *Solaris 7 vnode Paging Functions from* `vm/pvn.h`

| Function | Description |
|---|---|
| `pvn_getdirty()` | Queries whether a page is dirty. Returns 1 if the page should be written back (the iolock is held in this case), or 0 if the page has been dealt with or has been unlocked. |
| `pvn_plist_init()` | Releases the iolock on each page and downgrades the page lock to shared after new pages have been created or read. |
| `pvn_read_done()` | Unlocks the pages after read is complete. The function is normally called automatically by `pageio_done()` but may need to be called if an error was encountered during a read. |
| `pvn_read_kluster()` | Finds the range of contiguous pages within the supplied address / length that fit within the provided vnode offset / length that do not already exist. Returns a list of newly created, exclusively locked pages ready for I/O. Checks that clustering is enabled by calling the `segop_kluster()` method for the given segment.<br><br>On return from `pvn_read_kluster`, the caller typically zeroes any parts of the last page that are not going to be read from disk, sets up the read with `pageio_setup` for the returned offset and length, and then initiates the read with `bdev_strategy()`. Once the read is complete, `pvn_plist_init()` can release the I/O lock on each page that was created. |
| `pvn_write_done()` | Unlocks the pages after write is complete. For asynchronous writes, the function is normally called automatically by `pageio_done()` when an asynchronous write completes. For synchronous writes, `pvn_write_done()` is called after `pageio_done` to unlock written pages. It may also need to be called if an error was encountered during a write. |
