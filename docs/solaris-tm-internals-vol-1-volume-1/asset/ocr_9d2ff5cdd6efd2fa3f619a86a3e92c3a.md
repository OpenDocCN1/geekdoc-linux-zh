the number of physical reads and writes out of the buffer cache, and the read/write hit ratios.

```
```text
# sar -b 3 333
SunOS zangie 5.7 Generic sun4u4    06/27/99

22:01:51 bread/s lread/s %cache bwrit/s lwrit/s %wcache pread/s pwrit/s
22:01:54       0      7118     100       0       0      100       0       0
22:01:57       0      7863     100       0       0      100       0       0
22:02:00       0      7931     100       0       0      100       0       0
22:02:03       0      7736     100       0       0      100       0       0
22:02:06       0      7643     100       0       0      100       0       0
22:02:09       0      7165     100       0       0      100       0       0
22:02:12       0      6306     100       0      25       68       0       0
22:02:15       0      8152     100       0       0      100       0       0
22:02:18       0      7982     100       0       0      100       0       0
```
```

On this system we can see that the buffer cache is caching 100 percent of the reads and that the number of writes is small. This measurement was taken on a machine with 100 gigabytes of files that are being read in a random pattern. You should aim for a read cache hit ratio of 100 percent on systems with only a few, but very large, files (e.g., database systems) and a hit ratio of 90 percent or better for systems with many files.

# 15.2 Page Cache and Virtual Memory System

The virtual memory system is implemented around the page cache, and the file system makes use of this facility to cache files. This means that to understand file system caching behavior, we need to look at how the virtual memory system implements the page cache.

The virtual memory system divides physical memory into chunks known as pages; on UltraSPARC systems, a page is 8 kilobytes. To read data from a file into memory, the virtual memory system reads in one page at a time, or “pages in” a file. The page-in operation is initiated in the virtual memory system, which requests that file’s file system to page in a page from storage to memory. Every time we read in data from disk to memory, we cause paging to occur. We see the