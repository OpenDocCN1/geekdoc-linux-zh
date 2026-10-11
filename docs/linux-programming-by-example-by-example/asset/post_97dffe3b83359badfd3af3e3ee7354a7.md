
## Example

```c
/*
 * mp1ex.c - read input from pipe1 and pipe2 using select
 *
 * Adapted from mpx-select.c, written
 * by Michael Johnson and Erik Troan. Used with the permission of
 * the authors of _Linux Application Development,
 * Michael Johnson and Erik Troan.
 */
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

#define BUFSZ 80

void err_quit(char *msg);

int main(void)
{
    int fds[2];
    char buf[BUFSZ];
    int i, rc, maxfd;
    fd_set watchset;              /* Read this set of file descriptors */
    fd_set inset;                 /* Copy of watchset for select to update */

    /* Open the pipes */
    if((fds[0] = open("pipe1", O_RDONLY | O_NONBLOCK)) < 0)
        err_quit("open pipe1");
    if((fds[1] = open("pipe2", O_RDONLY | O_NONBLOCK)) < 0)
        err_quit("open pipe2");

    /* Initialize watchset with our file descriptors */
    FD_ZERO(&watchset);
    FD_SET(fds[0], &watchset);
    FD_SET(fds[1], &watchset);
    /* select needs to know the maximum file descriptor */
    maxfd = fds[0] > fds[1] ? fds[0] : fds[1];

    /* Loop while watching the pipes for output to read */
    while(FD_ISSET(fds[0], &watchset) || FD_ISSET(fds[1], &watchset)) {
        /* Make sure select has a current set of descriptors */
        inset = watchset;
        if(select(maxfd + 1, &inset, NULL, NULL, NULL) < 0)
            err_quit("select");

        /* Which file descriptor is ready to read? */
        for(i = 0; i < 2; ++i) {
            if(FD_ISSET(fds[i], &inset)) {
                rc = read(fds[i], buf, BUFSZ - 1);
                if(rc > 0) { /* Read some data */
                    buf[rc] = '\0';
                    printf("read: %s", buf);
                } else if(rc == 0) { /* This pipe is closed */
                    close(fds[i]);
                    FD_CLR(fds[i], &watchset);
                } else
                    err_quit("read"); /* Bummer */
            }
        }
    }
    exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

Figure 8.1 shows how `mplex` looks when it’s running.

This program is somewhat complex. After opening the two named pipes, it initializes a set of file descriptors using `FD_ZERO`, and then adds the descriptors for the two pipes. The heart of `mplex` is the `while` loop. During each iteration, it uses `FD_ISSET` to see if either of the pipes has data that can be read. If so, it first copies `watchset` to `inset` because `watchset` might have changed due to one of the pipes being closed.

![](img/be588b36b489136ce784030a08a1d3d4_203_0.png)

Figure 8.1: *mplex* multiplexes input from two pipes.

Next comes the *select* call, followed by a *for* loop that determines which descriptor is ready to be read (the timeout value is *NULL*, so *select* blocks until data is ready to be read). The *for* loop then reads the pipe, displays the data. If *read* returns 0, the pipe has been closed, so *mplex* closes that file and removes it from the watchset. When the last pipe closes, *mplex* terminates.

## Memory Mapping Files

*Memory-mapped files* are an identical copy in memory of a disk file. The *inode* image corresponds byte for byte to the disk file. Memory-mapped files have two chief advantages. The first advantage is faster file I/O. Ordinary I/O such as the *read* and *write* system calls and the *fputs* and *fgets* library calls, copy the data through kernel buffers. Although Linux uses a fast, sophisticated disk-caching algorithm, the fastest disk access will always be slower than the slowest memory access. I/O operations on a memory-mapped file bypass the kernel buffers and, as a result, are much faster. They are also simpler to use because you can access the mapped file using pointers rather than the usual file manipulation functions.

The second advantage of memory-mapped files is data sharing. If multiple processes need to access the same data, it can be stored in a memory-mapped file. Effectively a shared memory model (see Chapter 16, "Shared Memory"), this makes the data independent of any single process and available to any process, and stores the region's contents in a disk file.

The function calls to manage memory mapping are defined in `<sys/mman.h>`. They include the following calls:

- `mmap`—Maps a disk file into memory
- `munmap`—Unmaps a file, deletes the memory image
- `msync`—Updates the disk file with data from the memory image
- `mprotect`—Limits access to the memory image
- `mlock`—Prevents a portion of the map from being swapped to disk
- `munlock`—Removes a previously set lock
- `mlockall`—Prevents any part of the memory image from being swapped to disk
- `munlockall`—Removes the lock set by mlockall

These function calls are discussed in greater detail in the following sections.

## Creating a Memory Map

To create a memory mapped file, call `mmap`. When you have finished using it, call `munmap` to delete the mapping from memory and return the memory to the operating system.

## Mapping a File

The `mmap` function maps a disk file into memory. It has the following prototype:

```c
void *mmap(void *start, size_t length, int prot, int flags,
       int fd, off_t offset);
```

`mmap` creates a memory image of the file referred to by the file descriptor `fd`. The memory image will start from `offset` bytes into the file. The argument `length` indicates how much of the file should be read into memory. To limit access to the memory map, you can set various protection levels using the `prot` argument. It can be a logical OR of one or more of the values in Table 8.1. The `flags` parameter sets several additional attributes for the memory map. It can be a logical OR of one or more of the values listed in Table 8.2. `mmap` returns a pointer to the memory region or -1 on failure.

### Table 8.1: Values for mmap's protection Parameter

| Protection | Description |
| :--------- | :--------- |
| PROT_NONE  | No access is allowed |
| PROT_READ  | Mapped region may be read |
| PROT_WRITE | Mapped region may be written |
| PROT_EXEC  | Mapped region may be executed |

> **NOTE** On the x86 architecture, PROT_EXEC implies PROT_READ, so PROT_EXEC is the same as specifying PROT_EXEC|PROT_READ.

### Table 8.2: Values for mmap's flags Parameter

| Flag | Description |
| :----- | :----- |
| MAP_ANONYMOUS | Creates an anonymous mapping, ignoring fd |
| MAP_FIXED | Fails if address is invalid or already in use |
| MAP_PRIVATE | Writes to region are process private |
| MAP_SHARED | Writes to region are copied to file |
| MAP_DENYWRITE | Disallows normal writes to file |
| MAP_GROWSDOWN | Grows the memory downward |
| MAP_LOCKED | Locks pages into memory |

`offset` is usually 0, indicating that the entire file should be mapped into memory. A memory region must be marked either private, with `MAP_PRIVATE`, or shared, with `MAP_SHARED`; the other values are optional. A private mapping makes any modifications to the region process private, so these modifications are not reflected in the underlying file or available to other processes. Shared maps, on the other hand, cause any updates to the memory region to be immediately visible to other processes that have mapped the same file.

To prevent writes to the underlying disk file, specify `MAP_DENYWRITE` (but note that this is not a POSIX value and as such is not portable). Anonymous maps, created with `MAP_ANONYMOUS`, do not involve a physical file and simply allocate memory for the process’s private use, such as a custom `malloc` implementation. `MAP_FIXED` causes the kernel to place the map at a specific address. If the address is already in use or otherwise unavailable, `mmap` fails. If `MAP_FIXED` is not specified and address is unavailable, the kernel will attempt to place the region elsewhere in memory. `MAP_LOCKED` allows processes with root privilege to lock the region into memory so it will never be swapped to disk.

![](img/be588b36b489136ce784030a08a1d3d4_207_0.png)

**NOTE**
User programs cannot use `MAP_LOCKED`. This is a security feature that prevents unauthorized processes from locking all available memory, thus bringing the system to a standstill (also known as a *denial of service* attack).

## Unmapping a File

When you have finished using a memory mapped file, call `munmap` to unmap the region and return the memory to the operating system. This function has the following prototype:

```c
int munmap(void *start, size_t length);
```

The `start` argument is a pointer to the beginning of the region to unmap, and `length` indicates how much of the region to unmap. After a memory block has been unmapped, further attempts to access the memory to which `start` points will cause a segmentation fault (the signal `SIGSEGV`). When a process terminates, all memory maps are unmapped. The `munmap` function returns 0 on success. On failure, it returns -1 and sets `errno`.

As odd as it might seem, `munmap` might fail for a couple of reasons. The most common reason is that `start` does not point to mapped memory. Another cause for `munmap` to fail is that `length` is too long and, as a result, bleeds into memory that is not mapped.

## Example

![](img/be588b36b489136ce784030a08a1d3d4_207_1.png)

This program, `mkmap`, maps and unmaps a file specified on the command line.

```c
/*
 * mkmap.c Create a memory mapped file
 */
#include <sys/types.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>

void err_quit(char *msg);

int main(int argc, char *argv[])
{
```
