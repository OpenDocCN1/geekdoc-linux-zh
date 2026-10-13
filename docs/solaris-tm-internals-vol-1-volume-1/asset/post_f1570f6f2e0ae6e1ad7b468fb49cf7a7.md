
With priority paging enabled, we can see the different behavior of the virtual memory system.

```
# ./readtest testfile&

# memstat -3
memory -------- paging -------- executable -- anonymous -- filesys -- cpu ---
free re  pi  po  pf  fr  de  sr  epi  epo  ef  api  apo  fpi  fpo  cpu us  sw  et  id
3616  6   0  760  0  752  0  673  0    0   0   0    0    0  760  0  752  2   3 95  0
3328  2 198  816  0  925  0 1265  0    0   0   0    0    0  816  0  925  2  10 88  0
3656  4 195  765  0  792  0  263  0    0   0   0    0    0  762  0  792  7  11 83  0
3712  4   0  757  0  792  0  186  0    0   0   0    0    0  757  0  792  1   9 91  0
3704  3   0  770  0  789  0  203  0    0   0   0    0    0  770  0  789  0   5 95  0
3704  4   0  757  0  805  0  205  0    0   0   0    0    0  757  0  805  2   6 92  0
3704  4   0  778  0  805  0  266  0    0   0   0    0    0  778  0  805  1   6 93  0
```

With the same test program, random reads on the file system again cause the system to page, and the scanner is actively involved in managing the pages, but now the scanner is freeing only file pages. The zeros in the executable and anonymous memory columns clearly show that the scanner is choosing file pages first. The activity shown in the fpi and fpo columns means that file pages are being read in and an equal number are freed by the page scanner to make room for more reads.

## 15.4 Paging Parameters That Affect File System Performance

When priority paging is enabled, you will notice that the file system scan rate is higher. Because the page scanner must skip over process private memory and executables, it needs to scan more pages before it finds file pages that it can steal. High scan rates are always found on systems that make heavy use of the file system and so should not be used as a factor for determining memory shortage. If you have Solaris 7, then the memstat command will reveal if you are paging to the swap device; such paging suggests that you are short of memory.

If you have high file system activity, then you will find that the scanner parameters are insufficient and will limit file system performance. To compensate, you must set the scanner parameters `fastscan` and `maxpgio` to allow the scanner to scan at a high enough rate to keep up with the file system.

By default, the scanner is limited by the `fastscan` parameter, which reflects the number of pages per second that the scanner can scan. It defaults to scan one-fourth of memory every second and is limited to 64 megabytes per second. The scanner runs at half of `fastscan` when memory is at `lotsfree`, which limits it to 32 megabytes per second. If only one in three physical memory pages is a file page, then the scanner will only be able to put 32 / 3 = 11 megabytes per second of memory on the free list, limiting file system throughput. So, to allow the page scanner to scan fast enough, increase `fastscan` to, say, one-fourth of memory, with an upper limit of 1 gigabyte per second. That upper limit translates to 131072 for the `fastscan` parameter.

The `maxpgio` parameter is the maximum number of pages the page scanner can push. `maxpgio` can also limit the number of file system pages that are pushed, thus limiting the write performance of the file system. If your system has sufficient memory, then we recommend setting `maxpgio` to something large, say, 1024. On the E10000 systems, this is the default for `maxpgio`. For example, on a 4-gigabyte machine, one-fourth of memory is 1 gigabyte, so we would set `fastscan` to 131072. Our parameters, set in `/etc/system`, for this machine are shown below.

```
*
* Parameters to allow better file system throughput
*
set fastscan=131072
set handspreadpages=131072
set maxpgio=1024
```

In summary, we have seen a strong relationship between the VM system and file system behavior. The parameters that control the paging system have the most influence on file system performance, since they govern the way pages are made available to the file system. Figure 15.3 depicts the paging parameters that affect file systems and the memory parameters that control paging as the amount of free memory falls to the point where it hits these parameters.

When free memory falls below `cachefree`, file pages (which are not mapped executable) are freed. The scanner starts scanning at a rate of `slowscan`.

When free memory falls below this threshold, the system starts freeing all writes and UFS read-ahead is disabled.

When free memory falls below `lotsfree`, the scanner starts freeing anonymous (application heap) and executable pages in addition to file pages. This only happens when the scanner is not able to keep up with the rate of file system I/O.

If free memory falls to `desfree`, then NFS version 3 stops writing asynchronously, kernel async I/O stalls, and idle processes are swapped out.

When free memory falls below `cachefree`, pages that are not mapped executable are freed. The scanner starts scanning at a rate governed by `slowscan`.

Noncritical memory requests are blocked.

All memory requests are blocked.

The earth stops rotating if `freemem==0`.

![](img/220ae4af07df2fe8e5be69d27f885d1b_654_0.png)

(Parameters are measured in units of pages.)

- `cachefree`
- `lotsfree + pages_before_pager`
- `lotsfree`
- `desfree`
- `minfree`
- `throttlefree`
- `(60) pageout_reserve`
- `0`
- `slowscan`

The rate at which pages are made available to the file system varies with the scan rate and is capped by `fastscan` or 95% of 1 CPU.

- `fastscan`

**Figure 15.3** *VM Parameters That Affect File Systems*

## 15.5 Bypassing the Page Cache with Direct I/O

In some cases we may want to do completely unbuffered I/O to a file. A direct I/O facility in most file systems allows a direct file read or write to completely bypass the file system page cache.

### 15.5.1 UFS Direct I/O

Support for direct I/O was added to UFS starting with Solaris 2.6. Direct I/O allows reads and writes to files in a regular file system to bypass the page cache and access the file at near raw disk performance. Direct I/O can be advantageous when you are accessing a file in a manner where caching is of no benefit. For example, if you are copying a very large file from one disk to another, then it is likely that the file will not fit in memory and you will just cause the system to page heavily. By using direct I/O, you can copy the file through the file system without reading through the page cache and eliminate the memory pressure caused by the file system and the additional CPU cost of the layers of cache.

Direct I/O also eliminates the double copy that is performed when the read and write system calls are used. When we read a file through normal buffered I/O, the file system (1) uses a DMA transfer from the disk controller into the kernel’s address space and (2) copies the data into the buffer supplied by the user in the read system call. Direct I/O eliminates the second step by arranging for the DMA transfer to occur directly into the user’s address space.

Direct I/O will only bypass the buffer cache if all of the following are true:

- The file is not memory mapped.
- The file is not on a logging file system.
- The file does not have holes.
- The read/write is sector aligned (512 byte).

You enable direct I/O by mounting an entire file system with the `forcedirectio` mount option, as shown below.

```
# mount -o forcedirectio /dev/dsk/c0t0d0s6 /u1
```

You can also enable direct I/O with the `directio` system call, on a per-file basis. Note that the change is file based, and every reader and writer of the file will be forced to use directio once it’s enabled.

```
int directio(int filedes, DIRECTIO_ON | DIRECTIO_OFF);
```

**Header File**  `<sys/fcntl.h>`

Direct I/O can provide extremely fast transfers when moving data with big block sizes (>64 kilobytes), but it can be a significant performance limitation for smaller sizes. If an application reads and writes in small sizes, then its performance may suffer since there is no read-ahead or write clustering and no caching.

Databases are a good candidate for direct I/O since they cache their own blocks in a shared global buffer and can arrange to do their own clustering of reads and writes into larger operations.

A set of direct I/O statistics is provided with the ufs implementation by means of the kstat interface. The structure exported by `ufs_directio_kstats` is shown below. Note that this structure may change, and performance tools should not rely on the format of the direct I/O statistics.

```
struct ufs_directio_kstats {
        uint_t  logical_reads;   /* Number of fs read operations */
        uint_t  phys_reads;      /* Number of physical reads */
        uint_t  hole_reads;      /* Number of reads from holes */
        uint_t  readbytes;       /* Physical bytes read */
        uint_t  logical_writes;  /* Number of fs write operations */
        uint_t  phys_writes;     /* Number of physical writes */
        uint_t  writehits;       /* Number of write hits */
        uint_t  nflushes;        /* Number of times cache was cleared */
} ufs_directio_kstats;
```

You can inspect the direct I/O statistics with an engineering utility from our web-site at http://www.solarisinternals.com.

```
# directstat 3
        reads l writes dreads pwrites       Krd       Kw h oldrus mflush
             0       0       0       0         0         0       0      0
             0       0       0       0         0         0       0      0
             0       0       0       0         0         0       0      0
```

### 15.5.2 Direct I/O with Veritas VxFS

VxFS also provides a direct I/O implementation, which by default switches on whenever the read or write size is 256 kilobytes or greater. This VxFS feature is known as discovered direct I/O.

## 15.6 Directory Name Cache

The directory name cache caches path names for vnodes, so that when we open a file that has been opened recently, we don’t need to rescan the directory to find the file name again. Each time we find the path name for a vnode, we store it in the directory name cache. (See “The Directory Name Lookup Cache (DNLC)” on
