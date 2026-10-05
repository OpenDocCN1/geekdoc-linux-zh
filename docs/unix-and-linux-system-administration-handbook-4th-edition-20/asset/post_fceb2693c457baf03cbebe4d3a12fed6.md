
# Filesystem terminology

take extra steps to ensure cache coherency among computers. By default, cluster-features are turned off; use the -o cluster option to mount to turn them on.
HFS is HP's previous mainstream filesystem. It's based on the UNIX File System and is now deprecated, though still supported.

# AIX's JFS2

JFS2 is another filesystem that traces its roots back to the Berkeley Fast System. The J stands for “journaled,” but JFS2 has other tricks up its sleeve, including entries, dynamic allocation of inodes, and the use of a B+ tree structure to store directory entries.
JFS2 is also interesting in that it's available under the GNU General Public License. It runs on Linux, too.

# Filesystem terminology

Largely because of their common history with UFS, many filesystems share descriptive terminology. The implementations of the underlying objects have changed, but the terms are still widely used by administrators as labels for fundamental concepts.

“Inodes” are fixed-length table entries that each hold information about one file. They were originally preallocated at the time a filesystem was created, but some filesystems now create them dynamically as they are needed. Every way, inode usually has an identifying number that you can see with -i.

Inodes are the “things” pointed to directory entries. When you create a hard link to an existing file, you create a new directory entry, but you do not create a new inode.

On systems to preallocate inodes, you must decide how many to create. It's impossible to predict exactly how many will be needed, so filesystem-building commands use an empirical formula, based on the size of the volume and an average file size, to estimate an appropriate number. If you are anticipating trillions of small files, you may need to increase this number.

A superblock is a record that describes the characteristics of the filesystem. It contains information about the length of a disk block, the size and location of the inode tables, the disk block map and usage information, the size of the block groups, and few other important parameters of the filesystem. Because damage the superblock could erase some crucial information, several copies of it are maintained in scattered locations.

Filesystems cache disk blocks to increase efficiency. All types of blocks can be cached, including superblocks, inode blocks, and directory information. Caches are normally not “write-through,” so there may be some delay between the point at which an application thinks it has written a block and the point at which block is actually saved to disk.

# Chapter 8 Storage

Applications can request more predictable behavior for a file, but this lowers throughput.

The sync system flushes modified blocks to their permanent homes on disk, possibly making the on-disk filesystem fully consistent for a split second. Periodic save minimizes the amount of data loss that might occur if the machine were to crash with many unsaved blocks. Filesystems can sync on their own schedule or leave this to the OS. Modern filesystems have journaling mechanisms that minimize or eliminate the possibility of structural corruption in the event of a crash, so sync frequency now has to be with how many data blocks might be lost in a crash.

A filesystem's disk map is a table of the free blocks it contains. When new files are written, this map is examined to devise an efficient layout scheme. The block usage records basic information about the blocks that are already in use. In filesystems that support extent, the information may be significantly more complex than the simple bitmap used by other filesystems.

# Filesystem polymorphism

Filesystems are software packages with multiple components. One lives in the kernel (or even potentially in user space under Linux; google for FUSE) and implements the nuts and bolts of translating the filesystem API into writes of disk blocks. Other parts are user-level commands that initialize new volumes to the standard format, check filesystems for corruption, and perform other format-specific tasks.

Long ago, the standard user-level commands knew about "the filesystem" that the system used, and they simply implemented the appropriate functionality. mkfs created filesystems, fsck fixed problems, and mount just invoked the underlying system calls. These filesystems are more modular, so these commands call filesystem-specific implementations of each utility.

The exact implementation varies. For example, the Linux wrappers for directory-commands made mkfs, fsname, fsck, fsname and so on the normal directories for system commands. (You can run these commands directly, but it's rarely necessary.) AIX has a central /etc/vfs switch that records metainformation for filesystems (not to be confused with Solaris's /etc/vstab, which is equivalent to the fstab or systems file on other systems; it's not needed for ZFS).

# mkfs: format filesystems

The general recipe for creating a new filesystem

```
mkfs [-T ftype] [- options] rawdevice
```

The default fs may be hard-coded into the wrapper, or it might be specified in /etc/default/fs. The available options are filesystem specific, but it's that you'll need to use them. Linux uses it instead of -T, it omits the -T designator, and does not have raw device files. AIX uses -V instead of -T.

# fsck: check and repair filesystems

AIX crfs can allocate a new logical volume, create a filesystem on it, and update /etc/filesystems all in one step.

Two options you may consider tweaking are those that enable snapshots for filesystems that support them. The JFS2 can be de-fragmented and de-fragmented.
