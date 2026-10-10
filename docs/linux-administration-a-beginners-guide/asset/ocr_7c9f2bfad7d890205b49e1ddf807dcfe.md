# Chapter 6: The Command Line

# 119

| **Options for find** | **Description** |
| :--- | :--- |
| `-mount` | Do not search file systems other than the one from which search starts. |
| `-atime n` | File was accessed at least n*24 hours ago. |
| `-ctime n` | File was changed at least n*24 hours ago. |
| `-inum n` | File has i-node n. |
| `-amin n` | File was accessed n minutes ago. |
| `-cmin n` | File was changed n minutes ago. |
| `-empty` | File is empty. |
| `-mmin n` | File was modified n minutes ago. |
| `-mtime n` | File was modified n*24 hours ago. |
| `-nouser` | File’s UID does not correspond to a real user in /etc/passwd. |
| `-nogroup` | File’s GID does not correspond to a real group in /etc/group. |
| `-perm mode` | File’s permissions are exactly set to *mode*. |
| `-size n[\{ck]} | File is at least n blocks/characters/kilobytes. One block equals 512 bytes. |
| `-print` | Print the filenames found. |
| `-exec cmd\;` | On every file found, execute *cmd*. Important: Be sure to always follow every *cmd* with the \; characters, or BASH will become confused. |
| `-name name` | File’s name should be *name*. You can use regular expressions here. |

![](bbox=[0.13, 0.74, 0.92, 0.77])

Table 6-4 shows the most common parameters for dd. 

To generate an image of a floppy disk (especially useful for foreign file formats):

```
```shell
[root@ford /root]# dd if=/dev/fd0 of=/tmp/floppy_image
```
```