# sar 1203

%busy, avque

Portion of time device was busy servicing a transfer request, average number of requests outstanding during that time.

read/s, write/s, blks/s

Number of read/write transfers from or to device, number of bytes transferred in 512-byte units.

avseek Number of milliseconds per average seek.

For more-general system statistics, use iostat(1M), sar(IM), or vmstat(1M). See System Administration Guide: Basic Administration for naming conventions for disks.

+   -e time Select data up to time. Default is 18:00.

+   -f filename Use filename as the data source for sar. Default is the current daily data file /usr/adm/sa/sadd

+   -g Report paging activities:

+   pgout/s Page-out requests per second.
pgout/s Paged out per second.
pgfree/s Pages per second placed on the free list by the page-stealing daemon.
pgcan/s Pages per second scanned by the page-stealing daemon.

+   %ufs_ipf The percentage of UFS inodes that were taken off the free list by iget and have reusable pages associated with them. These pages are flushed and cannot be reclaimed by processes. Thus, the value is the percentage of gets with page flushes.

+   -i sec Select data at intervals as close as possible to sec seconds.

+   -k Report kernel memory allocation (KMA) activities.

+   sml_mem, alloc, fail Information about the memory pool reserving and allocating space for small requests: the amount of memory in bytes that KMA has for the small pool, the number of bytes allocated to satisfy requests for the number of requests for small amounts of memory that were not satisfied (failed).

+   lg_mem, alloc, fail Information for the large memory pool (analogous to the information for the small memory pool).