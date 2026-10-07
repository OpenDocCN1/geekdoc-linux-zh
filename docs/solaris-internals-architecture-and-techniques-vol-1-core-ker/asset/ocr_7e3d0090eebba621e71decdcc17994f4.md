# 602 option system call. Direct Solaris File System Cache

read system call. Direct I/O eliminates the second step by arranging for the DMA transfer to occur directly into the user's address space.

Direct I/O will only bypass the buffer cache if all of the following are true:

+   - The file is not memory mapped.
- The file is not on a logging file system.
- The file does not have holes.
- The read/write is sector aligned (512 byte).

You enable direct I/O by mounting an entire file system with the force-directio option, as shown below.

```
# mount -o directio /dev/dsk/c0t00s6 /ul
```

You can also enable direct I/O with the direct system call, on a per-file basis. Note that the change is file based, and every reader and writer of the file will be forced to use directio once it's enabled.

```
int directio(int ildes, DIRECTIO_ON | DIRECTIO_OFF);
```

# Header File <sys/fcntl.h>

Direct I/O can provide extremely fast transfers when moving data with big block sizes (>64 kilobytes), but it can be a significant performance limitation for smaller sizes. If an application reads and writes in small sizes, then its performance may suffer since there is no read-ahead or write clustering and no caching.

Databases are a good candidate for direct I/O since they cache their blocks in a shared global buffer and can arrange to do their own clustering of reads and writes into larger operations.

A set of direct I/O statistics is provided with the uds implementation by means of the kstat interface. The structure shown below. Note that this structure may change, and performance tools should not rely on the format of the direct I/O statistics.

```
struct uds_directio_kstat {
    uint_t logical_reads;      /* Number of fs read operations */
    uint_t phys_reads;        /* Number of physical reads */
    uint_t hole_reads;        /* Number of reads from holes */
    uint_t nread;             /* Physical bytes read */
    uint_t logical_writes;    /* Number of fs write operations */
    uint_t phys_writes;       /* Number of physical bytes written */
    uint_t nwrites;           /* Physical bytes written */
    uint_t nflushes;         /* Number of times cache was cleared */
} uds_directio_kstat;
```