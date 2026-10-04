+   - The group-id to which the file belongs
- The number of bytes in the file
- An array of 15 disk-block addresses
- The date and time the file was last accessed
- The date and time the file was last modified
- The date and time the file was created

The maximum number of files per UFS file system is determined by the number of inodes allocated for a file system. The number of inodes depends on how much disk space is allocated for each inode and the total size of the file system. By default, one inode is allocated for each 2KB of data space. You can change the default allocation by using the -i option of the newfs command.

# Storage Blocks

The rest of the space allocated to the file system is occupied by storage blocks, also called data blocks. The size of these storage blocks is determined at the time a file system is created. Storage blocks are allocated, by default, in two sizes: an 8KB logical block size and a 1KB fragmentation size.

For a regular file, the storage blocks contain the contents of the file. For a directory, the storage blocks contain entries that give the inode number and the filename of the files in the directory.

# Free Blocks

Blocks not currently being used as inodes, indirect address blocks, or storage blocks are marked as free in the cylinder group map. This map also keeps track of fragments to prevent fragmentation from degrading disk performance.

# How to Create a UFS File System

Use the newfs command to create UFS file systems. newfs is a convenient front-end to the mkfs command, the program that creates the new file system on a disk slice. On Solaris 2.x systems, information used to set some of the parameter defaults, such as number of tracks per cylinder and number of sectors per track, is read from the disk label. newfs determines the file system parameters to use, based on the options you specify and information provided in the disk label. Parameters are then passed to the mkfs (make file system) command, which builds the file system. Although you can use the mkfs command directly, it's more difficult to use and you must supply many of the parameters manually. The use of the newfs command is discussed later in this chapter.