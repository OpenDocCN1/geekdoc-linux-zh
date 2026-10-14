
8192 × (12 + 2048 + 2048² + 2048³) = 7.0403 × 10¹³ bytes

Thus, 70 trillion bytes should handle most users' needs.

File permissions are also contained in the inode information. We will cover the use of file permissions in our discussion of security in Chapter 11, “Networking and Security”.

## DIRECTORIES AND LINKS

Each inode is a pointer to a set of data. This concept is expressed as a link. A directory in UNIX is a file that contains a table of couplets. Each couplet is made up of an inode number and an identification string. The inode number points to an inode listing in the inode table, which in turn points to the data. The identification string is the filename associated with that set of data accessed via the inode. The pointers are shown in Figure 4.5.

![](img/415c89a1ede71e11e5040a0038b6916c_135_0.png)

Figure 4.5: Directory.

One of the most powerful features in UNIX is the concept of file links. There are two types of links: hard and soft. For a hard link, you have an entry in a directory file where the inode component of the couplet has the same inode number as another entry in that directory, or another directory on the same partition. By doing this, you have created two names that point to the same data. Once a hard link has been created, one name cannot have a greater ownership than any other name. Regardless of which name you use to modify a file, all the links point to the same data, so all the names associated with the inode will reflect the same data. Since each partition has a unique inode table, hard links cannot span partitions.

The second kind of link is a soft link, which is shown in Figure 4.6. In a soft link, the inode component of the directory couplet points to a unique inode in the inode table. It, in turn, has a reference to another inode stored in its first associated data block. The reference inode can be on any partition accessible to the file tree, regardless of what system it is located on. With symbolic links, the inode that points directly to the actual data block is the only official inode associated with the files; the other links are only references.

It does not matter how many hard links a data set accumulates; as long as one exists, the file exists. By contrast, if the original file/inode that is referenced by a symbolic link is removed, the symbolic link will now be pointing to nothing. Links are created with the ln command.

```
ln creates a hard link to a file
ln -s creates a soft link to a file
```

![](img/415c89a1ede71e11e5040a0038b6916c_136_0.png)

Figure 4.6: Symbolic links.

## FILE TYPES

The link structure means that everything in UNIX is actually a file. A directory is just a file that contains information relating to the filenames and inodes listed in the directory table. Likewise, a disk partition is represented in UNIX as a special file that contains information relating to the device drivers and disk information necessary to access the physical device. There are six major types of files in UNIX:

- Ordinary files.
- Directories.
- Links.
- Symbolic links.
- Named pipes.
- Special files.

Ordinary files can be anything from flat text documents to compressed archives. They can be considered as the leaves on the file tree. To be more specific, they are files that contain data in zero or more data blocks, not including addressing or redirection data. We discussed directories in the previous section. They are files in which the data is composed of inode-filename couplets. Links and symbolic links were also discussed. In the first case, the directory couplet is a direct reference to the inode table. In the latter case, the data block associated with the reference inode, in turn, references another inode entry.

Named pipes are FIFO (First In, First Out) structures. A named pipe makes it possible for one application to be writing data to a file while another application is reading the file. Special files do not contain any data. Instead, they provide an interface between physical devices and the filesystem. There are two types of special files: block and character files. A block file passes the data blocks received from a physical device, usually a disk, through the system buffer cache. The mount command requires block files. A character file transfers data directly from a device driver to a process without passing through the buffer cache. The fsck and newfs commands require character, or raw, files.
