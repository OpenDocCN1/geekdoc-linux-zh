# **11.3 Checking As the Real User: `access()`**

Most of the time, the effective and real UID and GID values are the same. Thus, it doesn't matter that file-permission checking is performed against the effective ID and not the real one.

However, when writing a setuid or setgid application, you sometimes want to check whether a file operation that's OK for the effective UID and GID is also OK for the *real* UID and GID. This is the job of the `access()` function:

```
#include <unistd.h>
POSIX

int access(const char *path, int amode);
```

The `path` argument is the pathname of the file to check the real UID and GID against. `amode` is the bitwise OR of one or more of the following values:

+   * `R_OK` The real UID/GID can read the file.
+   * `W_OK` The real UID/GID can write the file.
+   * `X_OK` The real UID/GID can execute the file, or if a directory, search through the directory.
+   * `F_OK` Check whether the file exists.

Each component in the pathname is checked, and on some implementations, when *checking for root*, `access()` might act as if `X_OK` is true, even if no execute bits are set in the file's permissions. (Strange but true: In this case, forewarned is forearmed.) Linux doesn't have this problem.

If `path` is a symbolic link, `access()` checks the file that the symbolic link points to.

The return value is 0 if the operation is permitted to the real UID and GID or –1 otherwise. Thus, if `access()` returns –1, a setuid program can deny access to a file that the effective UID/GID would otherwise be able to work with:

```
if (access("/some/special/file", R_OK|W_OK) < 0) {
   fprintf(stderr, "Sorry: /some/special/file: %s\n", strerror(errno));
   exit(1);
}
```

At least with the 2.4 series of Linux kernels, when the `X_OK` test is applied to a filesystem mounted with the noexec option (see Section 8.2.1, “Using Mount Options,” page 239), the test succeeds if the file's permissions indicate execute permission. This is true even though an attempt to execute the file will fail. Caveat emptor.