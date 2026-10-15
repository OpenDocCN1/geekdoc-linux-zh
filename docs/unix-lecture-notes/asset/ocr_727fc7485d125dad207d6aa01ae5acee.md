```
$ rm users
rm: remove users (yes/no)? y
$ ls -li
total 4
628 lrwxrwxrwx 1 sweiss student 5 Aug 30 00:22 ulist -> users
614 -rw------- 1 sweiss student 676 Aug 30 00:22 whoson
$ more ulist
ulist: No such file or directory
```

you see that ulist still points to users, even though it does not exist. This is not an error. The error only occurs when the process tries to access the file.

# 3.15.9 System Calls Related to Symbolic Links

The following system calls are related to the use of symbolic links.

```
#include <unistd.h>
int symlink(const char *oldpath, const char *newpath);
int readlink(const char *path, char *buf, size_t bufsiz);
int lstat(const char *file_name, struct stat *buf);
```

The system call that creates symbolic links is symlink(). The readlink() call obtains the name of the file to which a symbolic link is pointing. The lstat() call obtains a stat structure for a file that is a link, not the file to which it is linked.

# 3.16 Tree Walks

There are four different ways that we can visit all of the nodes in a given subtree of the hierarchy:

+   - Write our own recursive function to traverse the tree;
+   - Write a non-recursive function to traverse the tree;
+   - Use the nftw() POSIX library function;
+   - Use the fts() function available in systems including the 4.4BSD API.

Commands such as grep, chmod, chown, rm, cp, and chgrp use the fts() functions to perform their recursive tree traversals. The GNU version of the ls command, written by Richard Stallman and David MacKenzie, uses internal stacks and queues to recurse the tree. The GNU find command, originally written by Eric Decker, uses mutually recursive functions whereas the versions on BSD systems use the fts() functions. In this section we describe the functions provided by the libraries, beginning with the POSIX nftw() function and following with fts().