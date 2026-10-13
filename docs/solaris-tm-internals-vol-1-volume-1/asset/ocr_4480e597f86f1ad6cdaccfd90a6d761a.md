tally when we look at the virtual memory statistics. For example, reading a file will be reflected in vmstat as page-ins.

```
```text
# ./rreadtest testfiles

# vmstat
      procs      memory           page             disk        faults       cpu
 r  b  w  swap   free  re  mf  pi  po  fr  de  sr  s0  --  --  in   sy   cs  us sy id
 0  0  0  50436  2064   5   0  81   0   0   0   0  15   0   0   0  168  361  69  1 25 74
 0  0  0  50508  1336  14   0 222   0   0   0   0  35   0   0   0  210  902 130 21 51 47
 0  0  0  50508   648  10   0 177   0   0   0   0  27   0   0   0  168  850 121  1 60 39
 0  0  0  50508   584  29  57  88 109   0   0   0   6  14   0   0  108 5284 120  7 72 20
 0  0  0  50508   484   0  50 249  96   0   0   0  18  33   0   0  199  542 124  0 50 50
 0  0  0  50508   492   0  41 260  70   0   0   0  56  34   0   0  209  649 122  1 49 50
 0  0  0  50508   472   0  58 253 116   0   0   0  45  33   0   0  198  566 122  1 46 53
```
```

In our example, we can see this by starting a program that does random reads of a file, we cause a number of page-ins to occur, as indicated by the numbers in the pi column of vmstat. Note that the free memory column in vmstat has dropped to a low value; in fact, the amount of free memory is almost zero. This situation occurs because the file system consumes a page of physical memory every time it pages in a page-sized chunk of a file. Have you ever noticed that when you boot your machine there is a lot of free memory, and as the machine is used, memory continually falls to zero, then just hangs there? Here is why: the file system is using all available memory to cache the reads and writes to each file—and it's completely normal.

Memory is put back on the free list by the page scanner, which looks for memory pages that have not been used recently. The page scanner runs when memory falls to a system parameter known as lotsfree. In this example, we can see from the scan rate (sr) column that the page scanner is scanning about 50 pages per second to replace the memory used by the file system.

There is no parameter equivalent to bufhwm for the page cache. The page cache simply grows to consume all available memory, which includes all process memory that has not been used recently by applications. The rate at which the system pages and the rate at which the page scanner runs are proportional to the rate at which the file system is reading or writing pages to disk. On large systems, you should expect to see large paging values—it's completely normal.

Consider a system that is reading 10 megabytes per second through the file system; this translates to 1,280 page-ins per second and means that the page scanner must scan enough memory to be able to free 1,280 pages per second. The page scanner must actually scan faster than 1,280 pages per second, since not all memory the page scanner comes across will be eligible for freeing (the page scanner only frees memory that hasn't been used recently). If the page scanner finds only one out of three pages eligible for freeing, then it would need to run at 3,840 pages per second. Don't worry about high scan rates; if you are using the file system heavily, then they are normal. There are many myths about high scan rates mean-