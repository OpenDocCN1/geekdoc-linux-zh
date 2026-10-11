"Maintaining the Filesystem," for information on links.) Use `ls -1` to determine the number of the inode for any file. For example, issuing the command `ls -1 MyFile` returns the following:

```
4144 MyFile
```

This means that the information about the file MyFile has an inode number of 4144. If an inode becomes corrupted, the file will no longer be accessible. Another way to see the inode number for a file is to use the stat command. Its syntax is

```
stat filename
```

Its output should look similar to the following:

```
File: 'mywhich'
Size: 101     Filetype: Regular File
Mode: (0775/-rwxrwxr-x)  Uid: ( 503/ hadden) Gid: ( 500/ hadden)
Device: 3,0   Inode: 147474  Links: 1
Access: Tue Oct 19 16:10:58 1999 (00019.19:52:38)
Modify: Fri May 28 09:02:47 1999 (00014.03:06:55)
Change: Fri Sep  3 17:20:37 1999 (00065.18:40:59)
```

The stat command reads the inode structure associated with the specified filename.

# Key Concept

Each file has an associated inode that contains the file's physical location and all its attributes except for its filename. Use either the `ls -1` or stat command to determine a file's inode.

# File Types

Linux supports several file types and uses the first character in the permission block to name the file type. Linux does not differentiate between files and directories in the inode table. The operating system knows whether the file is a regular file or a directory by the file type character. The most common file type characters used by Linux are listed in Table 3.6.

Table 3.6 The First Character of the Permission Block Identifies the File Type

| Character | Type of File |
|-----------|--------------|
| -         | Ordinary file|
| b         | Block device |
| c         | Character device |
| d         | Directory |
| l         | Link |