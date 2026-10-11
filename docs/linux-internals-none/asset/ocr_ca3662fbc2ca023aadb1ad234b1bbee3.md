Second, the kernel now allows the buffer cache and the page cache to share the same memory. The buffer cache has always been used to cache data being written to disk, because the write-back code relies on having the physical locations of the data available; the buffer cache is the only cache is suitable for physically tagged blocks. In older kernels, that task (the tagging of buffered blocks to physical addresses) required us to copy page-cache data into separate memory when writing it to disk, but that inefficiency is eliminated in 2.4.

Third, at long last, we have support for large (>2GB) files, by virtue of defining all the offsets into our caches in units of file system blocks rather than by byte offsets.

# The Common Data Structure Objects  
Instantiated by the Kernel

+   struct super_block—Represents an entire file system mounted at a  
+   certain mount point in the directory tree.

+   struct inode—Represents a single object (file, directory, etc.) within  
+   that file system.

+   struct file—Represents a particular opening of a file. A new struct  
+   file is created every time you open a file, so you can have many  
+   struct files attached to a single inode. A closed file won’t have any  
+   struct files, although inodes representing it may still exist in the  
+   kernel’s object cache.

+   struct dentry—Represents the result of a directory lookup, that is,  
+   looking up a certain name in a certain directory.

+   struct address_space—The primary data cache in Linux is the page  
+   cache, and all pages are indexed in the page cache by offsets within  
+   an address_space. Every file inode has its own address space  
+   assigned within the page cache to identify cached data as belonging to  
+   that inode.

+   struct page—The main page descriptor for the virtual memory sys-
+   item; struct pages are used extensively by cache and I/O manage-
+   ment functions.

+   struct buffer_head—Describes a buffer in the buffer cache. The  
+   buffer cache is used to cache certain metadata on a file system, which  
+   doesn’t correspond to a real file. Buffers represent cached contents of  
+   a physical disk, not cached contents of files (files are virtual objects).  
+   For example, the buffer cache is used when we cache bitmaps or inode  
+   tables under most disk file systems. It is never used for network file  
+   systems—only when there is a disk involved.