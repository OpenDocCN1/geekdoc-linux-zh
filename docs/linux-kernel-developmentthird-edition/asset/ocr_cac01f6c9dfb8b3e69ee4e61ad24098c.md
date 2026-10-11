VFS Objects and Their Data Structures 265

# VFS Objects and Their Data Structures

The VFS is object-oriented.² A family of data structures represents the common file model. These data structures are akin to objects. Because the kernel is programmed strictly in C, without the benefit of a language directly supporting object-oriented paradigms, the data structures are represented as C structures. The structures contain both data and pointers to filesystem-implemented functions that operate on the data. The four primary object types of the VFS are

+   - the superblock object, which represents a specific mounted filesystem.
+   - the inode object, which represents a specific file.
+   - the dentry object, which represents a directory entry, which is a single component of a path.
+   - the file object, which represents an open file as associated with a process.

Note that because the VFS treats directories as normal files, there is not a specific directory object. Recall from earlier in this chapter that a dentry represents a component in a path, which might include a regular file. In other words, a dentry is not the same as a directory, but a directory is just another kind of file. Got it?

An operations object is contained within each of these primary objects. These objects describe the methods that the kernel invokes against the primary objects:

+   - The super_operations object, which contains the methods that the kernel can invoke on a specific filesystem, such as write_inode() and sync_fs()
+   - The inode_operations object, which contains the methods that the kernel can invoke on a specific file, such as create() and link()
+   - The dentry_operations object, which contains the methods that the kernel can invoke on a specific directory entry, such as d_compare() and d_delete()
+   - The file_operations object, which contains the methods that a process can invoke on an open file, such as read() and write()

The operations objects are implemented as a structure of pointers to functions that operate on the parent object. For many methods, the objects can inherit a generic function if basic functionality is sufficient. Otherwise, the specific instance of the particular filesystem fills in the pointers with its own filesystem-specific methods.

² People often miss this, or even deny it, but there are many examples of object-oriented programming in the kernel. Although the kernel developers may shun C++ and other explicitly object-oriented languages, thinking in terms of objects is often useful. The VFS is a good example of how to do clean and efficient OOP in C, which is a language that lacks any OOP constructs.