```
int fstat(int fildes, struct stat *buf);
```

# DESCRIPTION

These functions return information about the specified file. You do not need any access rights to the file to get this information but you need search rights to all directories named in the path leading to the file.

stat stats the file pointed to by file_name and fills in buf.

lstat is identical to stat, except in the case of a symbolic link, where the link itself is stat-ed, not the file that it refers to.

fstat is identical to stat, only the open file pointed to by fildes (as returned by open(2)) is stat-ed in place of file_name.

They all return a stat structure which has the following fields:

| mode_t | st_mode; | /* File mode (see mknod(2)) */ |
| ino_t | st_ino; | /* Inode number */ |
| dev_t | st_dev; | /* ID of device containing a */
|  |  | /* directory entry for this file */ |
| dev_t | st_rdev; | /* ID of device */
|  |  | /* This entry is defined only for */
|  |  | /* char special or block special files */ |
| nlink_t | st_nlink; | /* Number of links */ |
| uid_t | st_uid; | /* User ID of the file's owner */ |
| gid_t | st_gid; | /* Group ID of the file's group */ |
| off_t | st_size; | /* File size in bytes */ |
| time_t | st_atime; | /* Time of last access */ |
| time_t | st_mtime; | /* Time of last data modification */ |
| time_t | st_ctime; | /* Time of last file status change */ |
|  |  | /* Times measured in seconds since */ |
|  |  | /* 00:00:00 UTC, Jan. 1, 1970 */ |
| long | st_blksize; | /* Preferred I/O block size */ |
| blkcnt_t | st_blocks; | /* Number of 512 byte blocks allocated */ |

In short, we pass the stat() or lstat() function the pathname to the file and it fills in the stat structure pointed to by the second argument. If the pathname is not absolute, stat() and lstat() treat it as relative to the working directory. This is important, because if we pass it just a filename, the working directory of the process must be the one containing that filename. If a file is a symbolic link, lstat() displays information about the link itself, rather than the file to which it points, so if we want our program to behave like the real ls, we should use lstat() instead of stat().

There is more information returned by a call to one of the stat() functions than is displayed by ls -l, so we have to select which members of the stat structure we need to display. If you were wondering, the POSIX description of the structure in Section (3P) is similar. It will point out

> 11In fact, the POSIX page now contains example source code that solves the ls problem.