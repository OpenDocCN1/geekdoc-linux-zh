# Chapter 14 • Extended Interfaces

```
```
struct flock {
    ...
    short l_type;
    short l_whence;
    off_t l_start;
    off_t l_len;
    pid_t l_pid;
    ...
};
```
```

The `l_start` field is the starting byte offset for the lock. `l_len` is the length of the byte range, that is, the total number of bytes to lock. `l_whence` specifies the point in the file that `l_start` is relative to; the values are the same as for the `whence` argument to `lseek()` (see Section 4.5, “Random Access: Moving Around within a File,” page 102), hence the name for the field. The structure is thus self-contained: The `l_start` offset and `l_whence` value are *not* related to the current file offset for reading and writing. Some example code might look like this:

```
```
struct employee { /* whatever */
                struct flock lock;
};

/* Lock sixth struct employee */
lock.l_whence = SEEK_SET;
lock.l_start = 5 * sizeof(struct employee);
lock.l_len = sizeof(struct employee);
```
```

Using `SEEK_CUR` or `SEEK_END`, you can lock ranges relative to the current position in the file, or relative to the end of the file, respectively. For these two cases, `l_start` may be negative, as long as the absolute starting position is not less than zero. Thus, to lock the last record in a file:

```
```
/* Lock last record in a file */
lock.l_whence = SEEK_END;
lock.l_start = -1 * sizeof(struct employee);
lock.l_len = sizeof(struct employee);
```
```

Setting `l_len` to 0 is a special case. It means lock the file from the starting position indicated by `l_start` and `l_whence` through the end of the file. This includes any positions past the end of the file, as well. (In other words, if the file grows while the lock is held, the lock is extended so that it continues to cover the entire file.) Thus, locking the entire file is a degenerate case of locking a single record:

```
```
lock.l_whence = SEEK_SET;
lock.l_start = 0;
lock.l_len = 0;
```
```