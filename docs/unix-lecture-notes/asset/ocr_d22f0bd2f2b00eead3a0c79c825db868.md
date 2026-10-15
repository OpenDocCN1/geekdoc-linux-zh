```
int main(int argc, char *argv[])
{
    int     fd;

    /* create a new file named file_with_hole in the pwd */
    if ((fd = creat("file_with_hole", 0644)) < 0)
        exit(1);

    /* put a small string at the beginning */
    if (write(fd, buffer, 10) != 10)
        exit(1);

    /* seek 131072 = 2^17 bytes past the beginning of the file */
    if (lseek(fd, 131072, SEEK_SET) == -1)
        exit(1);

    /* write a small string there as well. */
    if (write(fd, enddata, 10) != 10)
        exit(1);

    /* we now have a large file with a big hole. */
    exit(0);
}
```

If you do an ls -sl on the file file_with_holes you will see that its size is 131082 bytes and uses 12 blocks. A block is usually 1KB.

```
$ ls -sl file_with_hole
12 -rw-r--r-- 1 stewart stewart 131082 Feb 21 20:09 file_with_hole
```

# 3.13.6 Modification and Access Time

Every i-node maintains three timestamps:

+   - st_mtime, the time the file was last modified
+   - st_ctime, the time the file attributes were last modified
+   - st_atime, the time the file was last read

These three timestamps are set by the kernel as the file is accessed and modified. You have no control over st_ctime, but you can change st_atime and st_mtime manually using the utime() system call:

```
#include <sys/types.h>
#include <utime.h>
int utime(const char *path, const struct utimbuf *times);
```