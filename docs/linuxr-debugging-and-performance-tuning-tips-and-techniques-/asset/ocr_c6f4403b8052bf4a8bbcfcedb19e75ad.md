96 Chapter 4 • Files and File I/O

96 Chapter 4 • Files and File I/O

# ### 4.4.2.2 Closing All Open Files

Open files are inherited by child processes from their parent processes. They are, in effect, *shared*. In particular, the position in the file is shared. We leave the details for discussion later, in Section 9.1.1.2, “File Descriptor Sharing,” page 286.

Since programs can inherit open files, you may occasionally see programs that close all their files in order to start out with a “clean slate.” In particular, code like this is typical:

```
int i;

/* leave 0, 1, and 2 alone */
for (i = 3; i < getdtablesize(); i++)
    (void) close(i);
```

Assume that the result of `getdtablesize()` is 1024. This code works, but it makes (1024 − 3) * 2 = 2042 system calls. 1020 of them are needless, since the return value from `getdtablesize()` doesn’t change. Here is a better way to write this code:

```
int i, fds;

for (i = 3, fds = getdtablesize(); i < fds; i++)
    (void) close(i);
```

Such an optimization does not affect the readability of the code, and it can make a difference, particularly on slow systems. In general, it’s worth looking for cases in which loops compute the same result repeatedly, to see if such a computation can’t be pulled out of the loop. In all such cases, though, be sure that you (a) preserve the code’s correctness and (b) preserve its readability!

# ### 4.4.3 Reading and Writing

I/O is accomplished with the `read()` and `write()` system calls, respectively:

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>

size_t read(int fd, void *buf, size_t count);
size_t write(int fd, const void *buf, size_t count);
```

POSIX