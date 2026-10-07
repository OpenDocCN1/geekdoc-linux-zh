
# Table 13-2 Solaris 7 Vnode Interface Methods from sys/vnode.h (Continued)

| Method | Description |
|---|---|
| vop_link() | Creates a hard link to the supplied vnode. |
| vop_lookup() | Looks up the path name for the supplied vnode. vop_lookup() does file-name translation for the open, stat system calls. |
| vop_map() | Maps a range of pages into an address space by doing the appropriate checks and calling as_map(). |
| vop_readdir() | directory of the of. name. |
| vop_open() | Opens a file referenced by the supplied vnode. open() system call has already done a vop_lookup() on the path name, returned a vnode pointer and then calls to vop_open(). This function typically does very little, since most of the real work was performed by vop_lookup(). |
| vop_pageio() | Paged I/O output for file system swap files. |
| vop_pathconf() | Establishes file system parameters with the pathconf system call. |
| vop_poll() | File system for the poll() system call. |
| vop_putpage() | Writes pages in the range offset and length for the vnode to the backing store of the file system. Does the real work of reading a vnode. |
| vop_read() | Reads the range supplied for the given vnode. read() typically maps the requested range of a file into kernel memory and uses vop_get_page() to do the real work. |
| vop_readlink() | Follows the synonym in the supplied vnode. |
| vop_realvp() | Gets the real vnode from the supplied vnode. |
| vop_remove() | Removes the file for the supplied vnode. |
| vop_rename() | Renames the file to the new name. |
| vop_rmdir() | Removes a directory pointed to by the supplied vnode. |
| vop_rwlock() | Holds the reader/writer lock for the supplied vnode. This method is called for each read(), with the rwflag set to 0 inside a read() system call and the rwflag set to 1 inside a write() system call. POSIX semantics require only one writer write() at a time. Some file system implementations have options to ignore the writer lock inside vop_rwlock(). |
| vop_runlock() | Releases the reader/writer lock for the supplied vnode. |
| vop_seek() | Seeks within the supplied vnode. |
| vop_setattr() | Sets the attributes for the supplied vnode. |

### ### 13-2 Solaris 7 vnode Interface Methods from sys/vnode.h (Continued)

| Method | Description |
|---|---|
| vopsetfl() | Sets file locks on the supplied vnode. |
| vopsetcatattr() | Sets security access control list attributes. |
| vopshrlock() | ONC shared lock support. |
| vopspace() | Frees space for the supplied vnode. |
| vopsymlink() | Creates a symbolic link between the two path names. |
| vopwrite() | Writes the range supplied for the given vnode. The write system typically maps the requested range of a file into kernel memory and uses vop_putpage to do the real work. |

### 13.2.3 vnode Reference Count

A vnode is created by the file system at the time a file is first opened and stays active until the file system decides the vnode is no longer needed. The vnode framework provides an infrastructure that keeps track of the number of references to a vnode. The kernel maintains the reference count by means of VN_HOLD() and VN_RELE() macros, which increment and decrement the v_count field of the vnode. A vnode stays while its reference count is greater than zero, so a subsystem can rely on a vnode's contents by calling VN_HOLD() before it references a vnode's contents. It is important to distinguish a vnode reference from a lock; a lock ensures exclusive access to the data, and the reference count ensures persistence of the object.

When a vnode's reference count drops to zero, VN_RELE() invokes VOP_INACTIVE() method for file system. Every subsystem is required to call VN_HOLD() at the start of the reference and call VN_RELE() at the end of each reference. Some systems deconstruct a vnode when its reference count falls to zero; others hold on the vnode for a while so if it is required again, it is available in its constructed state. The UFS file system, holds on the vnode for a while after the last release so that the virtual memory system can keep the inode and cache for a file, whereas the PCFS file system frees the vnode and all of the cache associated with the vnode at the time VOP_INACTIVE() is called.

### 13.2.4 Interfaces for Paging vnode Cache

Solaris unis file and memory management using a vnode to represent the backing store for virtual memory. A page of memory represents a particular vnode and offset. The file system uses the memory relationship to implement caching for vnodes within a file system. To cache a vnode, the file system has the memory system create a page of physical memory that represents the vnode and offset.

The virtual memory system provides a set of functions for cache management and I/O for vnodes. These functions allow the file systems to cluster pages for I/O handle the setup and checking required for syncing dirty pages with their backing store. The functions, described in Table 13-3, set up pages so that they can be passed to device driver block I/O handlers.

# Table 13-3 Solaris 7 vnode Paging Functions from vm/pvn.h

| Function | Description |
|---|---|
| pvn_getdirty() | Queries whether a page is dirty. Returns 1 if the page should be written back (the iolock is held in this case), or 0 if the page has been dealt with or has unlocked. |
| pvn_plist_init() | Releases the iolock on each page and the page lock to shared after new pages have been created or read. |
| pvn_read_done() | Unlocks the page after read is complete. The function is normally called automatically by pageio_done() but may need to be called if an error was encountered during a read. |
| pvn_read_kluster() | Finds the range of contiguous pages within the supplied address / length that fit within the provided vnode offset / length that do not already exist. Returns a list of newly created, locked pages ready for I/O. Checks that clustering is enabled by calling the segop_kluster() method for the segment |
| pvn_write_done() | Unlocks the page after write is complete. For asynchronous writes, the function is normally called automatically by pageio_done() when the write completes. For synchronous writes, it may need to be called if an error was encountered during a read. |

# Table 13-3 Solaris 7 vnode Paging Functions from vm/pvn.h (Continued)

| Function | Description |
|---|---|
| | | Returns a list of dirty locked pages ready for written back. On return from pvn_kluster(), the caller typically sets up the write with pageio_setup for the returned offset and length, initiates the write with bdev_strategy(). If the write is synchronous, then the caller should call pvn_write_done() to unlock the pages. If the write is asynchronous, then the io routine calls pvn_write_done() when the write completes |
| | | Finds all dirty pages in the page cache that have an offset greater than the supplied offset and calls the supplied putpage() routine. pvn_vplist_dirty() is often used to synchronize all dirty pages for a vnode when vop_putpage is called with a zero length |

### 13.2.5 Block I/O on vnode Pages

The block I/O subsystem provides support for initiating I/O to and from vnode pages. Three functions, shown in Table 13-4, initiate I/O between a physical page and a device.

# Table 13-4 Solaris 7 Paged I/O Functions from sys/bio.h

| Function | Description |
|---|---|
| bdev_strategy() | Initiates an I/O on a page, using the block I/O device |
| pageio_done() | Waits for the block device I/O to complete |
| pageio_setup() | Sets up a block buffer for I/O on a page of memory so it bypasses the block buffer cache by setting the B_PAGEIO flag and putting the page list on the b_pages field |

### 13.3 The vfs Object

The vfs layer provides an administrative interface into the file system to support commands like mount and unmount in a file-system-independent manner. The
