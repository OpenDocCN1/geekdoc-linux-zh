With priority paging enabled, we can see the different behavior of the virtual memory system.

```
# ./readtest testfile&

# memstat -3
memory -------- paging -------- executable -- anonymous -- filesys -- cpu ---
free re  ...  po  pg  fr  de  sr  epi  epo  ef  api  apo  fpi  fpo  cpu us  sw  et  id
3616  6  0  760  0  752  0  673  0  0  0  0  0  0  760  0  752  2  3 95  0
3328  2 198  816  0  925  0 1265  0  0  0  0  0  0  816  0  925  2 10 88  0
3656  4 195  765  0  792  0  263  0  0  0  0  0  0  762  0  792  7 11 83  0
3712  4  0  757  0  792  0  186  0  0  0  0  0  0  757  0  792  1  9 91  0
3704  3  0  770  0  789  0  203  0  0  0  0  0  0  770  0  789  0  5 95  0
3704  4  0  757  0  805  0  205  0  0  0  0  0  0  757  0  805  2  6 92  0
3704  4  0  778  0  805  0  266  0  0  0  0  0  0  778  0  805  1  6 93  0
```

With the same test program, random reads on the file system again cause the system to page, and the scanner is actively involved in managing the pages, but now the scanner is freeing only file pages. The zeros in the executable and anonymous memory columns clearly show that the scanner is choosing file pages first. The activity shown in the fpi and fpf columns means that file pages are being read in and an equal number are freed by the page scanner to make room for more reads.

# 15.4 Paging Parameters That Affect File System Performance

When priority paging is enabled, you will notice that the file system scan rate is higher. Because the page scanner must skip over process private memory and executables, it needs to scan more pages before it finds file pages that it can steal. High scan rates are always found on systems that make heavy use of the file system and so should not be used as a factor for determining memory shortage. If you have Solaris 7, then the memstat command will reveal if you are paging to the swap device; such paging suggests that you are short of memory.

If you have high file system activity, then you will find that the scanner parameters are insufficient and will limit file system performance. To compensate, you must set the scanner parameters fastscan and maxpgio to allow the scanner to scan at a high enough rate to keep up with the file system.

By default, the scanner is limited by the fastscan parameter, which reflects the number of pages per second that the scanner can scan. It defaults to scan one-fourth of memory every second and is limited to 64 megabytes per second. The scanner runs at half of fastscan when memory is at lot free, which limits it to 32 megabytes per second. If only one in three physical memory pages is a file page, then the scanner will only be able to put 32 / 3 = 11 megabytes per second of memory on the free list, limiting file system throughput. So, to allow the page scanner