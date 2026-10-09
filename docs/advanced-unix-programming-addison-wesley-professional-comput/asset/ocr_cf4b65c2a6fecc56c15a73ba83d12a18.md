+   *   To always copy a directory and its subtree, followed by a deletion of the old directory, even if the directory is just renamed within its parent.
+   *   A `link` system call that will work on directories, even if restricted to the superuser (The `mv` command can run with the set-user-ID bit on, to temporarily take on the privileges of the superuser.)
+   *   A new system call that can rename a directory within a file system

The first alternative is bad—that’s way too much work if all you want to do is change a few characters in the name! The second was ruled out by POSIX in favor of the third—a new system call, `rename`. Actually, it isn’t new—it was in Standard C and had been in BSD. It’s the only way to rename a directory without a full `copy`/`unlink`.

```
rename—rename file

#include <stdio.h>

int rename(
         const char *oldpath,         /* old pathname */
         const char *newpath          /* new pathname */
      );
/* Returns 0 on success or -1 on error (sets errno) */
```

rename is roughly equivalent to the sequence:

+   1.  If `newpath` exists, remove it with `unlink` or `rmdir`.
+   2.  `link(oldpath, newpath)`, even if `oldpath` is a directory.
+   3.  Remove `oldpath` with `unlink` or `rmdir`.

What `rename` brings to the table are some additional features and rules:

+   *   As I mentioned, step 2 works on directories, even if the process isn’t running as the superuser. (You need write permission in `newpath`’s parent, though.)
+   *   If `newpath` exists, it and `oldpath` have to be both files or both directories.
+   *   If `newpath` exists and is a directory, it has to be empty. (Same rule as for `rmdir`.) In step 3, `oldpath`, if a directory, is removed even if nonempty, since its contents are also in `newpath`.
+   *   If `rename` fails somewhere along the way, everything is left unchanged.

So you can see that while steps 1, 2, and 3 look like you could write them as a library function, there’s no way to get it to work like the system call.