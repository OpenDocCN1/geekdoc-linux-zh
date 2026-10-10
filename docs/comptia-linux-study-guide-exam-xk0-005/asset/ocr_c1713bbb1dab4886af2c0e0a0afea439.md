# **TABLE 15.4**	Linux file and directory attributes (_continued_)

| **Attribute** | **Description** |
|---|---|
| e | Linux is using extents for mapping blocks on the disk. |
| E | The file is encrypted by the file system. |
| F | When applied to a directory, all path lookups in the directory are case-insensitive. |
| i | The file can't be modified or deleted. |
| I | Index the directory using a hash tree. |
| j | If the file system supports journaling, data written to the file is written to the journal before being written to the file. |
| N | The file contains data stored in the inode table itself. |
| P | When applied to a directory, files in the directory inherit the project ID of the directory. |
| s | If the file is deleted, its blocks are zeroed and written back to the disk. |
| S | Changes to the file are written synchronously to the disk and not stored in a buffer. |
| t | If the file contains a partial block fragment at the end, it will not be merged with other files. |
| T | The directory is deemed the top of a directory hierarchy for storage purposes. |
| U | Save the contents of the file when deleted, allowing for the undelete feature. |
| V | Apply file authentication to the file. |

To assign an attribute to a file or directory you precede the attribute with a plus sign:

```
```
$ sudo chattr +i test1.txt
$ rm test1.txt
rm: cannot remove 'test1.txt': Operation not permitted
$ 
```
```

This example sets the immutable attribute ( i ) to a file, making it impossible to delete the file. This particular attribute can only be set by the root user account, thus the need to use the sudo command. After setting the attribute, the file can no longer be deleted.