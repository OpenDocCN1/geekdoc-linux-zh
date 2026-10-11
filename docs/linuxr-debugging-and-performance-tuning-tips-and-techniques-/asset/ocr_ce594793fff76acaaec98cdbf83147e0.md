```
```
lock_l_whence = ... ; /* As before */
lock_l_start = ... ; /* As before */
lock_l_len = ... ; /* As before */
lock_l_type = F_UNLCK; /* Unlock */
if (fcntl(fd, F_SETLKW, & lock) < 0) {
    /* handle error */
}
/* Lock has been released*/
```
```

Code using lockf() is a bit simpler. For brevity, we’ve omitted the error checking:

```
```
off_t cursor, len;

cursor = lseek(fd, (off_t) 0, SEEK_CUR); Retrieve current position
len = ... ; Set correct number of bytes to lock

lockf(fd, F_LOCK, len); Acquire lock
... use locked area here ...
lseek(fd, cursor, SEEK_SET); Return to position of lock

lockf(fd, F_ULOCK, len); Unlock file
```
```

If you don’t explicitly release a lock, the operating system will do it for you in two cases. The first is when the process exits (either by `main()` returning or by the `exit()` function, which was covered in Section 9.1.5.1, “Defining Process Exit Status,” page 300). The other case is when you call `close()` on the file descriptor; more on this in the next section.

# 14.2.2.3 Observing Locking Caveats

There are several caveats to be aware of when doing file locking:

+   - As described previously, advisory locking is just that. An uncooperative process can do anything it wants behind the back (so to speak) of processes that are doing locking.
+   - These calls should *not* be used in conjunction with the `<stdio.h>` library. This library does its own buffering, and while you can retrieve the underlying file descriptor with `fileno()`, the actual position in the file may not be where you think it is. In general, the Standard I/O library doesn’t understand file locks.
+   - Bear in mind that locks are *not* inherited by child processes after a `fork` but that they *do* remain in place after an `exec`.