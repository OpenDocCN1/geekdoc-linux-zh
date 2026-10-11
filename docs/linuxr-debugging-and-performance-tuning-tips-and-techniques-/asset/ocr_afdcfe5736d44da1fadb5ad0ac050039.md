+   | `st_atime_nsec` | The nanoseconds component of the file’s access time. |
+   | `st_mtime_nsec` | The nanoseconds component of the file’s modification time. |
+   | `st_ctime_nsec` | The nanoseconds component of the file’s inode change time. |

Some other systems also provide such high-resolution time fields, but the member names for the struct stat are not standardized, making it difficult to write portable code that uses these times. (See Section 14.3.2, “Microsecond File Times: utimes(),” page 545, for a related advanced system call.)

# 5.4.4 Determining File Type

Recall that the st_mode field encodes both the file’s type and its permissions. <sys/stat.h> defines a number of macros that determine the file’s type. In particular, these macros return true or false when applied to the st_mode field. The macros correspond to each of the file types described earlier. Assume that the following code has been executed:

```
```
struct stat stbuf;
char filename[PATH_MAX];   /* PATH_MAX is from <limits.h> */
... fill in filename with a file name ...
if (stat(filename, & stbuf) < 0) {
    /* handle error */
}
```
```

Once stbuf has been filled in by the system, the following macros can be called, being passed stbuf.st_mode as the argument:

+   `S_ISREG(stbuf.st_mode)`
+     Returns true if filename is a regular file.

+   `S_ISDIR(stbuf.st_mode)`
+     Returns true if filename is a directory.

+   `S_ISCHR(stbuf.st_mode)`
+     Returns true if filename is a character device. Devices are shortly discussed in more detail.

+   `S_ISBLK(stbuf.st_mode)`
+     Returns true if filename is a block device.

+   `S_ISFIFO(stbuf.st_mode)`
+     Returns true if filename is a FIFO.