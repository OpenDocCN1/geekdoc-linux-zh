# UFS Implementation

vert a vnode pointer to an inode pointer, and the macro ITOV to convert an inode
to to a vnode pointer.

```
/*
 * Convert between inode pointers and vnode pointers
 * #define VTOI (VP)  ((struct inode *)(VP)->v_data)
 * #define ITOV (IP)  ((struct vnode *)(IP)->i_vnode)
```

Header File /ufs/inode.h

# 14.3.3.1 Freeing inodes—the Inode Idle List

When the last reference to a vnode is released, the vop_inactive() routine for the file system is called. (See vnode reference counts in "vnode Reference Count" on page 538.) UFS implements vop_inactive to free the inode when it is no longer required. UFS implements an idle list because if we were to destroy each vnode when the last reference to a vnode is relinquished, we would throw away all the data relating to that vnode, including all of the file pages cached in the page cache. This practice could mean that if a file is closed and then reopened, none of the file data that was cached would be available after the second open and would need to be reread from disk.

# 14.3.3.2 Caching Inodes—the Inode Idle List

Each time the last reference to a file is made, the vop_inactive() method for the file system is called to handle the last reference to the vnode. UFS implements an idle queue to cache recently closed inodes in their constructed state, to keep their in-kernel state and file system page caches intact.

For idling nodes, UFS implements a thread that maintains a list of idle inodes on a queue. The ufs_inactive() routine puts UFS inodes into the idle queue. The ufs is passed a vnode, and the UFS uses the ITOV macro to convert an inode reference, which is then placed onto the idle queue. The inodes on the idle queue retain all of their state, keeping all pages in the page cache in memory. The inodes stay on the idle queue until the idle queue reaches a watermark, at which point the UFS idle thread is awakened to free half of the inode idle queue. Figure 14.11 illustrates the process.