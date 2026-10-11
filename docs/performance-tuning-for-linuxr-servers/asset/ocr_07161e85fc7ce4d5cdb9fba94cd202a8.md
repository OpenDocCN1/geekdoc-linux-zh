Non-journaled file systems rely on fsck to examine all the file system's metadata and detect and repair structural integrity problems before restarting. If Linux shuts down smoothly, fsck typically returns a clean bill of health. However, after a power failure or crash, fsck is likely to find some kind of error in metadata.

Because file systems contain significant amounts of metadata, running fsck can be very time-consuming. fsck has to scan a file system's *entire* repository of metadata to ensure consistency and error-free operation; therefore, the speed of fsck on a disk partition is proportional to the size of the partition, the number of directories, and the number of files in each directory.

For large file systems, journaling becomes crucial. Journaled file systems provide improved structural consistency, better recovery, and faster restart times than non-journaled file systems. In most cases, journaled file systems can restart in less than a second.

# Transactions Are the Solution

The magic of journaling file systems lies in *transactions*. Like database transactions, journaling file system transactions treat a sequence of changes as a single, atomic operation. However, instead of tracking updates to tables, the journaling file system tracks changes to file system metadata or user data. The transaction guarantees that either *all* or *none* of the file system updates are done.

For *example*, the process of creating a new file modifies several metadata structures (inodes, free lists, and directory entries). Before the file system makes those changes, it creates a transaction that describes what it is about to do. After the transaction has been recorded (on disk), the file system goes ahead and modifies the metadata. The *journal* in a journaling file system is simply a list of transactions.

In the event of a system failure, the file system is restored to a consistent state by replaying the journal. Rather than examine *all* metadata (the fsck way), the file system inspects only those portions of the metadata that have recently changed. Recovery is much faster—usually only a matter of seconds. Better yet, recovery time is not dependent on the size of the partition.

In addition to faster restart times, most journaling file systems also address another significant problem: scalability. Combining even a few large-capacity disks, it is easy to assemble some massive (certainly by early-'90s standards) file systems. Features of modern file systems include the following:

+   - *Faster allocation of free blocks*. Extents (as described previously) and B+ trees are used individually or together to find and allocate several free blocks quickly, either by size or location.

+   - *Large (or very large) numbers of files in a directory*. A directory is a special file that contains a list of files. If a directory needs to contain thousands or tens of thousands of files, something better than a linked list of (name, inode) pairs is