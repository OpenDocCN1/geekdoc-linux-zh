# Filesystem terminology

take extra steps to ensure cache coherency among computers. By default, cluster-features are turned off; use the -o cluster option to mount to turn them on.
HFS is HP's previous mainstream filesystem. It's based on the UNIX File System and is now deprecated, though still supported.

# AIX's JFS2

JFS2 is another filesystem that traces its roots back to the Berkeley Fast System. The J stands for “journaled,” but JFS2 has other tricks up its sleeve, including entries, dynamic allocation of inodes, and the use of a B+ tree structure to store directory entries.
JFS2 is also interesting in that it's available under the GNU General Public License. It runs on Linux, too.

# Filesystem terminology

Largely because of their common history with UFS, many filesystems share descriptive terminology. The implementations of the underlying objects have changed, but the terms are still widely used by administrators as labels for fundamental concepts.

“Inodes” are fixed-length table entries that each hold information about one file. They were originally preallocated at the time a filesystem was created, but some filesystems now create them dynamically as they are needed. Every way, inode usually has an identifying number that you can see with -i

Inodes are the “things” pointed to directory entries. When you create a hard link to an existing file, you create a new directory entry, but you do not create a new inode.

On systems to preallocate inodes, you must decide how many to create. It's impossible to predict exactly how many will be needed, so filesystem-building commands use an empirical formula, based on the size of the volume and an average file size, to estimate an appropriate number. If you anticipating trillions of small files, you may need to increase this number.

A superblock is a record that describes the characteristics of the filesystem. It contains information about the length of a disk block, the size and location of the inode tables, the disk block map and usage information, the size of the block groups, and few other important parameters of the filesystem. Because damage the superblock could erase some crucial information, several copies of it are maintained in scattered locations.

Filesystems cache disk blocks to increase efficiency. All types of blocks can be cached, including superblocks, inode blocks, and directory information. Caches are normally not “write-through,” so there may be some delay between the point at which an application thinks it has written a block and the point at which