directly. As an example, here are the Linux synopses, which I won't bother to explain completely:

```
```
mount—mount file system (nonstandard)

#include <sys/mount.h>

int mount(
    const char *source,    /* device */
    const char *target,     /* directory */
    const char *type,       /* type (e.g., ext2) */
    unsigned long flags,    /* mount flags (e.g., MS_RDONLY) */
    const void *data        /* file-system-dependent data */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

```
```
umount — unmount file system (nonstandard)

#include <sys/mount.h>

int umount(
    const char *target     /* directory */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

Normally, umount fails with the error EBUSY if any file or directory on it is in use. There's usually an alternative system call named umount2 that has a flag as a second argument that forces the umount, which is occasionally essential when the system has to be shut down.

From the application-programming perspective, except for one situation, you're normally not concerned with the fact that a given file or directory you're trying to access is on a file system separately mounted from some other file or directory, as long as you have a path name that works. In fact, all accessible file systems, even the root, had to be mounted at one time, perhaps during the boot sequence. The one situation has to do with links, which is what the next section is about.

# 3.3 Hard and Symbolic Links

An entry in a directory, consisting of a name and an i-number, is called a hard link. The other kind of link is a symbolic link, which I'll talk about in a moment. Figure 3.3.3 illustrates both. (The hex numbers in parentheses are device IDs, which I'll explain later.)