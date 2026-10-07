with the respective range of the file. Once we are done with that range of the file, we may never want it it again, in which case we can let the operating system know that this memory range is no longer needed. This notification is especially important since the memory is not freed, when we unmap the memory segment. The MADV_DONTNEED flag allows us to give back memory for a given range. The following example shows how this can be done.

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/macros.h>
#include <sys/types.h>
#include <fcntl.h>
#include <sys/mman.h>

void
 main(int argc, char ** argv)
{
    int fd;
    caddr_t addr;
    off_t size;
    off_t length;
    off_t offset;
    off_t chunk = 1<<30;

    if (argc != 1) {
        (void) fprintf(stderr, "Usage: mmap_out filename\n");
        exit(1);
    }
    if ((fd = open(argv[1], O_RDONLY)) < 0) {
        perror("Open failed");
        exit(1);
    }

    size size = lseek64(fd, (off_t)0, SEEK_END);
    /*
     * mmap a chunkwise segment and issue madvise(DONTNEED)
     * against it.
     */
    for (offset = 0; offset < size; offset += chunk) {
        length = MIN(size - offset, chunk);
        if ((addr = mmap64((caddr_t)0, length, PROT_READ|PROT_WRITE,
                            MAP_SHARED, fd, offset)) == NULL) {
            perror("mmap failed");
            exit(1);
        }
        (void) madvise(addr, length, MADV_DONTNEED);
        (void) munmap(addr, length);
    }
}
```

We can execute the preceding program to free the range of a file back to the memory system. We can observe what happens when we run the program by looking at