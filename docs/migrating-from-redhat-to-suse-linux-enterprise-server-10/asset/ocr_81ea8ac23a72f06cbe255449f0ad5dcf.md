In the **Mount Point** field enter the *directory* where the partition should be mounted in the file system tree. If the directory does not exist yet, it is automatically created by YaST.

When you finish configuring the file system and mounting parameters, select **OK**, and **Apply** in the Expert Partitioner dialog.

A warning message appears cautioning you about committing the changes you have made. Choosing **Apply** commits the changes to disk and returns you to the Expert Partitioner, whereas **Finish** commits them and closes the Expert Partitioner.

# ## Create a File System with Command Line Tools

There are various commands to create file systems, including mk2fs, mkfs.ext3, and mkreiserfs. You can use these to create file systems, such as ext2, ext3, and ReiserFS.

The alternative is the command **mkfs**, which is a frontend for the actual commands that create file systems (such as mkfs.ext2, mkfs.ext3, or mkfs.msdos).

When using **mkfs**, you need to use the option **-t** to indicate the file system type you want to create. If you do not indicate a file system type, mkfs automatically creates an ext2 file system.

You need to know how to:

+   - Create an ext2 or ext3 File System
+   - Create a Reiser File System