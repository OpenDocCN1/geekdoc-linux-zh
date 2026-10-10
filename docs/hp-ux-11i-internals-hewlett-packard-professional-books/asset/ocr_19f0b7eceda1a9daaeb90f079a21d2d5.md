![](bbox=[0.15, 0.09, 0.85, 0.42])

Figure 8-6 Metadata

As we mentioned, the inode table was located in the middle of the disk to improve overall access time; but as not all disk drives are the same size, there needed to be a metadata structure in a well-known location on all disks containing potential file systems. To meet this need, several additional structures were created.

When a machine is booting, it is running from simplified code in its boot ROM. A boot ROM usually has very minimalist driver code and can read only the first block of a device. For this reason, the first block of the disk is reserved as a boot block. Next, a block called the super-block is allocated. The superblock contains static and dynamic information about the specifics of the file system on the disk. One of the most important components is a pointer to the starting address (a byte offset) of the inode table. Additional structures, such as bit allocation maps, are also assigned and mapped by the superblock. Each type of file system may have its own specific additions to the contents of the superblock but certain key values are located at fixed offsets within the superblock regardless of the file system type. These values are used by the kernel to identify the file system type, version, and basic static configuration data.

# Layering a Directory Hierarchy on a Flat File System

Another feature desired by the UNIX developers was the implementation of a hierarchical file system. The file structure was based on a basically flat model (there is only one inode table per file system), so a method needed to be developed to facilitate the use of directories and subdirectories.