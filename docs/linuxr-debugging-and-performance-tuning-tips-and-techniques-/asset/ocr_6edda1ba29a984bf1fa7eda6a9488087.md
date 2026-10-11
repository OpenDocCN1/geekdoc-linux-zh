For this reason, 4.2 BSD introduced the `rename()` system call:

```
#include <stdio.h>            ISO C
int rename(const char *oldpath, const char *newpath);
```

On Linux systems, the renaming operation is atomic; the manpage states:

> If `newpath` already exists it will be atomically replaced ..., so that there is no point at which another process attempting to access `newpath` will find it missing.

If `newpath` exists but the operation fails for some reason, `rename` guarantees to leave an instance of `newpath` in place.

However, when overwriting there will probably be a window in which both `oldpath` and `newpath` refer to the file being renamed.

As with other system calls, a `0` return indicates success, and a return value of `-1` indicates an error.

# 5.1.5 File Removal

Removing a file means removing the file’s entry in the directory and decrementing the file’s link count (maintained in the inode). The contents of the file, and the disk blocks holding them, are not freed until the link count reaches zero.

The system call is named `unlink():`

```
#include <unistd.h>        POSIX
int unlink(const char *pathname);
```

Given our discussion of file links, the name makes sense; this call removes the given link (directory entry) for the file. It returns `0` on success and `-1` on error.

The ability to remove a file requires write permission only for the directory and not for the file itself. This fact can be confusing, particularly for new Linux/Unix users. However, since the operation is one on the directory, this makes sense; it is the directory contents that are being modified, not the file’s contents.²

² Indeed, the file’s *metadata* are changed (the number of links), but that does not affect any other file attribute, nor does it affect the file’s contents. Updating the link count is the only operation on a file that doesn’t involve checking the file’s permissions.