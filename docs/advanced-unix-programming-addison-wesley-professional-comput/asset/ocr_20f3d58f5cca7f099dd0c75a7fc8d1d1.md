```
ec_null( dir = opendir(argv[i]) )
ec_neg1( fd = open("..", O_RDONLY) )
ec_neg1( chdir(argv[i]) )
while (errno = 0, !(entry = readdir(dir)) != NULL) {
    ec_neg1( lstat(entry->d_name, &statbuf) )
    ls_long(&statbuf, entry->d_name);
}
ec_nzero( errno )
ec_neg1( fchdir(fd) )
```

There’s still a problem. If you want to try to find it before I tell you what it is, stop reading *here*.

The problem is that if there’s an error between the `chdir` and `fchdir` calls that jumps to the cleanup code, the call to `fchdir` won’t be executed, and the current directory won’t be restored. It’s OK in this program because all such errors terminate the process, and the current directory is unique to each process. (The shell’s current directory won’t be affected.) But, still, if the error processing should be changed at some point, or if this code is copied and pasted into another program, things could go awry.

A good fix (not shown) is to put a second call to `fchdir` in the cleanup code, so it gets executed no matter what. You can initialize `fd` to −1 and test for that so you don’t use it unless it has a valid value.

# 3.6.3 **mkdir** and **rmdir** System Calls

There are two system calls for making and removing a directory:

```
**mkdir**—make directory

#include <sys/stat.h>
int mkdir(
    const char *path,         /* pathname */
    mode_t perms              /* permissions */
);
/* Returns 0 on success or −1 on error (sets errno) */
```

```
**rmdir**—remove directory

#include <unistd.h>
int rmdir(
    const char *path          /* pathname */
);
/* Returns 0 on success or −1 on error (sets errno) */
```