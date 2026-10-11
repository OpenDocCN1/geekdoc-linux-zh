
The `lockf()` function provides an alternative way to acquire a lock *at the current file position*:

```c
#include <sys/file.h> /* XSI */
int lockf(int fd, int cmd, off_t len);
```

The file descriptor, `fd`, must have been opened for writing. `len` specifies the number of bytes to lock: from the current position (call it `pos`) to `pos + len` bytes if `len` is positive, or from `pos - len` to `pos - 1` if `len` is negative. The commands are as follows:

- **F_LOCK**: Sets an exclusive lock on the range. The call blocks until the lock becomes available.
- **F_TLOCK**: Tries the lock. This is like F_LOCK, but if the lock isn’t available, F_TLOCK returns an error.
- **F_ULOCK**: Unlocks the indicated section. This can cause lock splitting, as described earlier.
- **F_TEST**: Sees if the lock is available. If it is, returns 0 and acquires the lock. Otherwise, it returns -1 and sets `errno` to EACCES.

The return value is 0 on success and -1 on error, with `errno` set appropriately. Possible error returns include:

- **EAGAIN**: The file is locked, for F_TLOCK or F_TEST.
- **EDEADLK**: For F_TLOCK, this operation would cause a deadlock.
- **ENOLCK**: The operating system is unable to allocate a lock.

The combination of F_TLOCK and EDEADLK is useful: If you know that there can never be potential for deadlock, then use F_LOCK. Otherwise, it pays to be safe and use F_TLOCK. If the lock is available, you’ll get it, but if it’s not, you have a chance to recover instead of blocking, possibly forever, waiting for the lock.

When you’re done with a lock, you should release it. With `fcntl()`, take the original struct lock used to acquire the lock, and change the l_type field to F_UNLCK. Then use F_SETLKW as the cmd argument:

```c
lock_l_whence = ... ; /* As before */
lock_l_start = ... ; /* As before */
lock_l_len = ... ; /* As before */
lock_l_type = F_UNLCK; /* Unlock */
if (fcntl(fd, F_SETLKW, & lock) < 0) {
    /* handle error */
}
/* Lock has been released */
```

Code using `lockf()` is a bit simpler. For brevity, we’ve omitted the error checking:

```c
off_t cursor, len;

cursor = lseek(fd, (off_t) 0, SEEK_CUR); /* Retrieve current position */
len = ... ; /* Set correct number of bytes to lock */

lockf(fd, F_LOCK, len); /* Acquire lock */
... use locked area here ...
lseek(fd, cursor, SEEK_SET); /* Return to position of lock */

lockf(fd, F_ULOCK, len); /* Unlock file */
```

If you don’t explicitly release a lock, the operating system will do it for you in two cases. The first is when the process exits (either by `main()` returning or by the `exit()` function, which was covered in Section 9.1.5.1, “Defining Process Exit Status,” page 300). The other case is when you call `close()` on the file descriptor; more on this in the next section.

### 14.2.2.3 Observing Locking Caveats

There are several caveats to be aware of when doing file locking:

- As described previously, advisory locking is just that. An uncooperative process can do anything it wants behind the back (so to speak) of processes that are doing locking.
- These calls should *not* be used in conjunction with the `<stdio.h>` library. This library does its own buffering, and while you can retrieve the underlying file descriptor with `fileno()`, the actual position in the file may not be where you think it is. In general, the Standard I/O library doesn’t understand file locks.
- Bear in mind that locks are *not* inherited by child processes after a `fork` but that they *do* remain in place after an `exec`.
- A `close()` of *any* file descriptor open on the file removes *all* of the process's locks on a file, even if other file descriptors remain open on it.

That `close()` works this way is unfortunate, but because this is how `fcntl()` locking was originally implemented, POSIX standardizes it. Making this behavior the standard avoids breaking existing Unix code.

### 14.2.3 BSD Locking: `flock()`

4.2 BSD Unix introduced its own file locking mechanism, `flock()`. It is declared as follows:

```c
#include <sys/file.h>          /* Common */
int flock(int fd, int operation);
```

The file descriptor `fd` represents the open file. These are the operations:

- **LOCK_SH**: Creates a shared lock. There can be multiple shared locks.
- **LOCK_EX**: Creates an exclusive lock. There can be only one such lock.
- **LOCK_UN**: Removes the previous lock.
- **LOCK_NB**: When bitwise-OR'd with `LOCK_SH` or `LOCK_EX` avoids blocking if the lock isn't available.

By default, the lock requests will block (not return) if a competing lock exists. Once the competing lock is removed and the requested lock is obtained, the call returns. (This implies that, by default, there is potential for deadlock.) To attempt to obtain a lock without blocking, perform a bitwise OR of `LOCK_NB` with one of the other values for operation.

The salient points about `flock()` are as follows:

- `flock()` locking is also advisory locking; a program that does no locking can come in and blast, with no errors, a file locked with `flock()`.
- The whole file is locked. There is no mechanism for locking or unlocking just a part of the file.
- How the file was opened has no effect on the type of lock that may be placed. (Compare this to `fcntl()`, whereby the file must have been opened for reading for a read lock, or opened for writing for a write lock.)
- Multiple file descriptors open on the same file share the lock. Any one of them can be used to remove the lock. Unlike `fcntl()`, when there is no explicit unlock, the lock is not removed until all open file descriptors for the file have been closed.
- Only one `flock()` lock can be held by a process on a file; calling `flock()` successively with two different lock types changes the lock to the new type.
- On GNU/Linux systems, `flock()` locks are completely independent of `fcntl()` locks. Many commercial Unix systems implement `flock()` as a “wrapper” on top of `fcntl()`, but the semantics are not the same.

We don't recommend using `flock()` in new programs, because the semantics are not as flexible and because the call is not standardized by POSIX. Support for it in GNU/Linux is primarily for compatibility with software written for older BSD Unix systems.

> **NOTE** The GNU/Linux `flock(2)` manpage warns that `flock()` locks do not work for remotely mounted files. `fcntl()` locks do, provided you have a recent enough version of Linux and an NFS server that supports locking.

### 14.2.4 Mandatory Locking

Most commercial Unix systems support mandatory file locking, in addition to advisory file locking. Mandatory locking works only with `fcntl()` locks. Mandatory locking for a file is controlled by the file’s permission settings, in particular, by addition of the setgid bit to a file with the `chmod` command:

```bash
$ echo hello, world > myfile
$ ls -l myfile
-rw-r--r-- 1 arnold devel 13 Apr 3 17:11 myfile
$ chmod g+s myfile
$ ls -l myfile
-rw-r--sx- 1 arnold devel 13 Apr 3 17:11 myfile
```

The group execute bit should be left turned off. The `s` shows that the setgid bit is turned on but that execute permission isn’t; an `x` would be used if both were on.

The combination of setgid on and group execute off is generally meaningless. For this reason, it was chosen by the System V developers to mean “enforce mandatory locking.” And indeed, adding this bit is enough to cause a commercial Unix system, such as Solaris, to enforce file locks.

On GNU/Linux systems, the story is a little different. The setgid bit must be applied to a file for mandatory locking, but that alone is not enough. The filesystem containing the file must also be mounted with the **mand** option to the **mount** command.

We have already covered filesystems, disk partitions, mounting, and the **mount** command, mostly in Section 8.1, “Mounting and Unmounting Filesystems,” page 228. We can demonstrate mandatory locking with a small program and a test filesystem on a floppy disk. First, here’s the program:

```c
/* ch14-10ckill.c --- Demonstrate mandatory locking. */

#include <stdio.h>           /* for fprintf(), stderr, BUFSIZ */
#include <errno.h>           /* declare errno */
#include <fcntl.h>           /* for flags for open() */
#include <string.h>          /* declare strerror() */
#include <unistd.h>          /* for ssize_t */
#include <sys/types.h>
#include <sys/stat.h>        /* for mode_t */

int
main(int argc, char **argv)
{
    int fd;
    int i, j;
    mode_t rw_mode;
    static char message[] = "hello, world\n";
    struct flock lock;

    if (argc != 2) {
        fprintf(stderr, "usage: %s file\n", argv[0]);
        exit(1);
    }

    rw_mode = S_IRUSR | S_IWUSR | S_IRGRP | S_IROTH;      /* 0644 */
    fd = open(argv[1], O_RDWR|O_TRUNC|O_CREAT|O_EXCL, rw_mode);
    if (fd < 0) {
        fprintf(stderr, "%s: %s: cannot open for read/write: %s\n",
                argv[0], argv[1], strerror(errno));
        (void) close(fd);
        return 1;
    }
```
