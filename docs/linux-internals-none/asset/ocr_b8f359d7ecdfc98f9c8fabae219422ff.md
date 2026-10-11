reflected on the media at any given time. These file systems rely on restart-time utilities (which in Linux usually means fsck), which examine all of the file system’s metadata (such as directories and disk addressing structures) to detect and repair structural integrity problems. This is a time-consuming and error-prone process, which, in the worst case, can lose or misplace data.

Journaling file systems keep track only of inode changes, but not changes to the contents of a file; whereas logging file systems keep track of changes made to both data and inodes. All changes, all appends, and all deletes would be logged to a growing part of the file system known as the log.

In our first example with the test.file file, rather than modifying the data in the 3506 block, a logging file system would store a copy of the inodes of both test.file and the third block in new locations on the disk.

The in-memory list of inodes would be changed to point test.file to the new inode as well. Every once in a while, the file system will check-point and update the on-disk list of inodes, as well as freeing the unused parts of files (e.g. the original third block of test.file).

A logging file system has a dramatically improved write speed because it’s only appending to the same area of the disk and never really needs to seek around looking for blocks on the disk.

The writing speed is therefore improved as is the recovery time (actually, there is no recovery time at all because of its structure).

Logging file systems, when compared to static file systems, have nearly identical read speed because their file data blocks are still easily seekable. The inode map has the lists of blocks, and those can be read quickly because they are usually memory mapped. Thus, logging file systems represent the best of both worlds. The read time is comparable to that of the static file system—well, possibly a bit slower due to more fragmentation: The major problem with logging file systems is that they can get fragmented easily.

# Metadata Logging

When a file system makes changes to its on-disk structure, it uses several disconnected, synchronous writes to make those changes. If an outage occurs halfway through an operation, the state of the file system is unknown, and the whole file system must be checked for consistency.