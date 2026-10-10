To find files that have been accessed in the last day, use

$ find path -atime -2 -print

+   - -ctime n. true if the file's status was changed n days ago.
+   - -empty true if the file is a plain file or directory and is empty.
+   - -fstype type true if the file system containing the file is of type type. Common values for type are ext2 for normal Linux file systems, proc for the /proc pseudo-file system, and iso9660 for CD-ROM file systems.
+   - -gid n true if the file's numeric group ID is n.
+   - -group gname true if the file's group is gname.
+   - -name pattern true if the file's base name (with leading directories removed) matches the shell pattern pattern.
+   - -iname pattern Like -name, but matching is case-insensitive.
+   - -mtime n true if the file's contents were last modified n days ago.
+   - -newer otherFile true if the file was modified more recently than otherFile.
+   - -perm mode true if the file's permission bits are exactly mode.
+   - -perm -mode true if all the bits in mode are set for the file.
+   - -perm +mode true if any of the bits set in mode are set for the file.
+   - -size n[bcwk] true if the file uses n units of space. A “unit” is 512 bytes, unless a letter follows n. In this case, c makes a unit one byte, k makes a unit one kilobyte, b makes a unit 512 bytes, and w makes a unit two bytes.
+   
+   For example, to find all files under your home directory that are larger than one megabyte, use
+   
+   $ find $HOME -size +1024k -print

+   - -type x true if the file is of type x, where x is one of the following:
+     - b A block device
+     - c A character device
+     - d A directory
+     - f A regular file
+     - l A symbolic link
+     - p A named pipe (FIFO)
+     - s A socket

![](bbox=[0.85, 0.2, 1.0, 0.6])