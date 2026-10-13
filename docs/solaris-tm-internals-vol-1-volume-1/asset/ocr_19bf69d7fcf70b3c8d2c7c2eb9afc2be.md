two states: either the inode is referenced, or the inode is no longer referenced but is on an idle queue. Inodes are eventually destroyed when they are pushed off the end of the inode idle queue. Refer to “Freeing inodes—the Inode Idle List” on page 598 for a description of how ufs inodes are maintained on the idle queue.

The number of inodes in memory is dynamic. Inodes will continue to be allocated as new files are referenced. There is no upper bound to the number of inodes open at a time; if one million inodes are opened concurrently, then a little over one million inodes will be in memory at that point. A file is referenced when its reference count is nonzero, which means either the file is open for a process or another subsystem such as the directory name lookup cache is referring to the file.

When inodes are no longer referenced (the file is closed and no other subsystem is referring to the file), the inode is placed on the idle queue and eventually freed. The size of the idle queue is controlled by the ufs_ninode parameter and is limited to one-fourth of ufs_ninode. The maximum number of inodes in memory at a given point is the number of active referenced inodes plus the size of the idle queue (typically, one-fourth of ufs_ninode). Figure 15.4 illustrates the inode cache.

![](bbox=[0.182, 0.426, 0.889, 0.654])

**Figure 15.4** *In-Memory Inodes (Referred to as the “Inode Cache”)*

We can use the sar command and inode kernel memory statistics to determine the number of inodes currently in memory. sar shows us the number of inodes currently in memory and the maximum reached. We can find similar information by