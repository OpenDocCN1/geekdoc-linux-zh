would provide, yet can describe files larger than can be stated in the bits used in the “size” parameter.

The inode of a *directory* refers to structured data held in the same kind of hierarchy of disk blocks as a plain file. This data consists of the names and inode numbers of plain files, special files and directories.

Because it is the inode which really establishes file data, it is trivial to have multiple directory entries referring to the same inode and thus to the same file. This reference is permitted for file types, but prohibited for directory types because of the confusion it would engender when searching a file system.

Until recently, directory data could be read just like data in other files, but because directories on networked file systems are not quite the same as directories on a local disk, this ability has been removed to enforce consistent directory access.

*Special files* to access peripherals come in two categories: block I/O entries and character I/O entries. Block I/O refers to random disk access. Character I/O entries are used to access the terminal, keyboard, display, modem, etc. Ken Thompson wrote

> In retrospect, the names [block I/O and character I/O] should have been ‘structured I/O’ and ‘unstructured I/O’, respectively[51].

If the type is a peripheral, either block I/O or character I/O, a major and minor number is given in place of pointers to disk blocks. The peripheral type selects which look-up table (block or character) to use. The major number indexes the appropriate table to identify which device driver will service the system call. The minor number identifies which specific device, such as a serial communication port or disk partition, is the subject of the I/O function.

Few user programs access block I/O devices directly because they usually contain the traditional file system and are accessed through the file system functions.

# 2.2.5 SUID

Another significant idea first seen in Unix, and issued U.S. patent number 4,135,240, is the “Set User ID bit” associated with each file.