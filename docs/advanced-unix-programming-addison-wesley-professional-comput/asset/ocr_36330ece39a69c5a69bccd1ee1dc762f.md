with an EACCES error because, as the effective user-ID is the superuser, it cannot fail for that reason.

+   • To check whether a file exists. You could use stat instead, but access is simpler. (Actually, the whole access system call could be written as a library function calling stat, and, in some implementations, it even might be implemented that way.)

If path is a symbolic link, that link is followed until a nonsymbolic link is found.[15]

When you call access, you probably don’t want to put it in an ec_neg1 macro because, if it returns –1, you’ll want to distinguish an EACCES error (for R_OK, W_OK, and/or X_OK) or an ENOENT error (for F_OK) from other errors. Like this:

```
if (access("tmp", R_OK) == 0)
    printf("Exist\n");
else if (errno == ENOENT)
    printf("Does not exist\n");
else
    EC_FAIL
```

# 3.8.2 mknod System Call

```
**mknod**—make file
```c
#include <sys/stat.h>
int mknod(
      const char *path,          /* pathname */
      mode_t perms,             /* mode */
      dev_t dev                 /* device-ID */
  );
/* Returns 0 on success or -1 on error (sets errno) */
```
```

mknod makes a regular file, a directory, a special file, or a named pipe (FIFO). The only portable use (and the only one for which you don’t need to be super-user) is to make a named pipe, but for that you have mkfifo (Section 7.2.1). You also don’t need it for regular files (use open) or for directories (use mkdir) either. You can’t use it for symbolic links (use symlink) or for sockets (use bind).

15. This is true of almost all system calls that take a pathname, unless they start with the letter I. Two exceptions are unlink and rename.