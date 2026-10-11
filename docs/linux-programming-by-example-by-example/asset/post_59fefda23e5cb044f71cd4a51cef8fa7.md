
int main(void)
{
    uid_t owner = 500;
    gid_t group = 100;
    int fd;

    /* create the file */
    if((fd = open("some.file", 0_CREAT, 0644)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }
    /* ls the file */
    system("ls -l some.file");
    /* change its ownership */
    if((fchown(fd, owner, group)) < 0) {
        perror("fchown");
        exit(EXIT_FAILURE);
    }
    /* ls it again */
    system("ls -l some.file");
    exit(EXIT_SUCCESS);
}

Here is the result of executing this program:

$ su
Password:
$ ./chgmod
-rw-r--r--    1 root    root         0 Jul 24 21:11 some.file
-rw-r--r--    1 kwall   users        0 Jul 24 21:11 some.file
$ exit

As you can see, the program first created the file. In the sample run, I first used the `su` command to become the superuser, so the file was created with root user and group ownership. The `fchown` command changes the owner and group to the specified values, 500 and 100, which correspond to kwall and users on my system. The second ls command confirms that the ownership was successfully changed.

### What's Next?

In this chapter, you learned a good deal about working with Linux's basic file-handling calls. The next chapter extends this discussion by covering advanced material about topics such as the ext2 filesystem, multiplexing, non-blocking I/O, memory-mapped files, and file and record locking. This will complete the discussion of Linux's file-handling interface, which prepares you to learn about a database API and shared memory.

## 8—Advanced Linux File Handling

This chapter continues the discussion of Linux’s file-handling interface that began in the last chapter, but covers more advanced features, such as the following:

- Manipulating file timestamps
- Features of Linux’s ext2 filesystem
- I/O multiplexing
- High-speed I/O using memory mapped files
- File locking

### Changing File Timestamps

Recall from Chapter 7, "Basic Linux File Handling," the kernel contains three timestamps for each file: its last access time (*atime*), last modification time (*mtime*), and last change time (*ctime*). The POSIX standard provides the *utime* routine to change the *atime* and the *mtime*. There is no user-level programmatic interface for changing the *ctime*, but changing the *atime* or *mtime* function causes the *ctime* to change, so it should not be a problem.

The *utime* function is prototyped in `<utime.h>` as

int utime(const char *pathname, struct utimbuf *buf);

You might also need to include the `<sys/types.h>` header file because it contains the primitive system data types defined by POSIX. Older versions of *gcc* and Linux did not always include `<sys/types.h>` in `<utime.h>`, so if your compiler complains about undefined values when compiling programs, add the types header file, but only if it declares the type about which the compiler complains. *utime* changes the access and modification times of the file specified by *pathname* to the *actime* and *modtime*, respectively, which are stored in *buf*. If *buf* is NULL, the *actime* and *modtime* are set to the current time. As usual, *utime* returns 0 on success. On error, it sets *errno* and returns -1. Of course, the process calling *utime* must have appropriate access to the file or be running with root privileges.

The *utimbuf* structure is defined as follows:

struct utimbuf {
    time_t actime;  /* access time */
    time_t modtime; /* modification time */
};

The *time_t* type is a POSIX standard type, usually a long integer, that stores the number of seconds elapsed since the Epoch. The *Epoch*, in turn, is defined by POSIX to be the date/time January 1, 1970 at 00:00:00 UTC (Universal Coordinated Time, which used to be known as Greenwich Mean Time).

> **NOTE** Interestingly, because many of Linux’s time-related functions are based on the Epoch, the much-publicized year 2000 bug is not as big a problem for Linux as is the year 2038. Because *time_t* is a long integer, it will overflow in 2038. That is, *time_t* can hold up to 2^31-1 seconds, or 2,147,483,647 seconds. Disregarding leap years, there are 365*24*60*60, or 31,536,000, seconds in each year. So, *time_t* represents a maximum of about 68 years (2,147,483,647 / 31,536,000). Because the epoch begins in 1970, adding 68 years to this yields 2038. The exact date and time when *time_t* will overflow varies, depending on how many seconds exist in leap years.

### Example

![](img/be588b36b489136ce784030a08a1d3d4_187_0.png)

The program that follows creates a file and sets its atime and mtime values to September 8, 2001. For the purposes of brevity, error checking has been omitted.

/*
 * chgttime.c - Using the utime routine
 */
#include <sys/types.h>
#include <sys/stat.h>
#include <utime.h>
#include <unistd.h>
#include <stdlib.h>
#include <fcntl.h>

int main(void)
{
    time_t now = 1000000000;
    struct utimbuf buf;
    int fd;

    buf.actime = now;
    buf.modtime = now;

    fd = open("foo.bar", O_CREAT, 0644);
    utime("foo.bar", &buf);
    close(fd);

    exit(EXIT_SUCCESS);
}

Running the program and then listing the current directory results in the following:

![](img/be588b36b489136ce784030a08a1d3d4_187_1.png)

### Output

$ ls -l foo.bar
-rw-r--r--  1 kwall users      0 Sep  8  2001 foo.bar

As you can see, foo.bar has a timestamp of September 8, 2001. After setting the atime and mtime members of the utimbuf structure to 1,000,000,000 (which corresponds to September 8, 2001), chgttime opens the file, then calls utime on it, passing the address of the modified structure and the filename. This causes the last access time and the last modification time (*actime* and *modtime*, respectively) to be changed to the specified (and utterly improbable) date and time.

### Features of the ext2 Filesystem

The ext2 filesystem enables you to set up to four special attributes on files:

- **Immutable**—`EXT2_IMMUTABLE_FL`
- **Append-only**—`EXT2_APPEND_FL`
- **No-dump**—`EXT2_NODUMP_FL`
- **Sync**—`EXT2_SYNC_FL`

Only the root user can set or remove the immutable and append-only flags, but a file's owner may set or clear the no-dump and sync flags. What do these flags mean? The following list describes them in detail:

- **Immutable** files cannot be modified at all: You can add data to them, remove or rename them, or add links to them. Not even the superuser can do these things—the immutable flag must first be cleared.
- **Append-only** files can be written only in append mode and cannot otherwise be removed, renamed, or linked.
- The **no-dump** attribute causes the `dump` command, commonly used for creating backups, to ignore a file.
- The **sync** attribute causes the file to be written synchronously; that is, all *writes* to the file must complete before returning to the calling process (this is identical to calling `open` with the `O_SYNC` option).

Why use these attributes? Making a file immutable prevents it from being accidentally (or deliberately) deleted or modified, so it is a handy security measure for critical files. The append-only flag preserves a file's current contents while still allowing you to add data to it—again, a handy security precaution.

The no-dump flag is simply a convenience that will save you valuable space and time when you back up a system. The sync flag, finally, is especially handy for guaranteeing that critical files, such as databases, actually get written when requested. Using the sync option prevents data loss if a system goes down before cached data is physically written to disk. The downside of the sync flag, however, is that it can significantly slow down a program's performance.

To get or set these attributes, use the `ioctl` call, declared in `<sys/ioctl.h>`. Its prototype is as follows:

int ioctl(int fd, int request, void *arg);
