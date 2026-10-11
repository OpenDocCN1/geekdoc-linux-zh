These system calls, as well as lchown(), are of relatively recent vintage;11 older Unix systems won’t have them, although modern, POSIX-compliant systems do.

There are no corresponding futime() or lutime() functions. In the case of futime(), this is (apparently) because the file timestamps are not critical to system security in the same way that ownership and permissions are. There is no lutime(), since the timestamps are irrelevant for symbolic links.

# ### 5.6 Summary

+   * The file and directory hierarchy as seen by the user is one logical tree, rooted at /. It is made up of one or more storage partitions, each of which contains a filesystem. Within a filesystem, inodes store information about files (metadata), including the location of file data blocks.

+   * Directories make the association between filenames and inodes. Conceptually, directory contents are just sequences of (inode, name) pairs. Each directory entry for a file is called a (hard) link, and files can have many links. Hard links, because they work only by inode number, must all be on the same filesystem. Symbolic (soft) links are pointers to files or directories that work based on filename, not inode number, and thus are not restricted to being on the same filesystem.

+   * Hard links are created with link(), symbolic links are created with symlink(), links are removed with unlink(), and files are renamed (possibly being moved to another directory) with rename(). A file’s data blocks are not reclaimed until the link count goes to zero and the last open file descriptor for the file is closed.

+   * Directories are created with mkdir() and removed with rmdir(); a directory must be empty (nothing left but ‘.’ and ‘..’) before it can be removed. The GNU/Linux version of the ISO C remove() function calls unlink() or rmdir() as appropriate.

+   * Directories are processed with the opendir(), readdir(), rewinddir(), and closedir() functions. A struct dirent contains the inode number and the file’s name. Maximally portable code uses only the filename in the d_name member. The BSD telldir() and seekdir() functions for saving and restoring the