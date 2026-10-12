swapping. So we increased the number of users or load on the environment. We also started to monitor and gather information about the servers.

After some time, when the load was at its peak, there were once again timed-out messages displayed on the Workload Simulator. But unlike the previous workload simulation, this time the vmstat tool did not report any swapping or high memory usage (see Example 11-8).

# **Example 11-8** *vmstat report without any swapping with 3 GB memory*

```
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
r  b   swpd   free    buff    cache si so bi bo in cs us sy id wa st
0  0  0  1561060 10516 235616  0  0  0  3  558 567 14 2 83 0  1
4  0  0  1476736 10548 235584  0  0  1  7  673 607 10 2 88 0  1
1  0  0  1379412 10572 235560  0  0  0  4  650 647 8  2 89 0  1
0  0  0  1273640 10600 235532  0  0  0  7  689 681 8  2 88 0  1
0  0  0  1175308 10616 235516  0  0  0  6  685 689 7  2 90 0  1
0  0  0  1078960 10636 235496  0  0  0  6  702 694 7  2 90 0  1
0  0  0  983935  10676 235456  0  0  0  3  680 684 11 2 86 0  1
1  1  0  886512  10704 235428  0  0  0  5  681 690 7  2 90 0  1
0  0  0  789720  10748 235900  0  0  0  5  683 696 7  2 90 0  1
0  0  0  693744  10788 235860  0  0  0  8  853 685 8  2 89 0  1
0  0  0  598410  10828 235820  0  0  0  2  723 688 7  2 90 0  1
0  0  0  500924  10872 235776  0  0  0  7  682 696 7  2 89 0  1
25 0  0  393160  10912 235736  0  0  0  2  672 681 12 2 85 0  1
0  0  0  392788  10952 235696  0  0  0  7  660 715 11 2 86 0  1
0  0  0  392788  10992 235656  0  0  0  3  658 694 7  2 90 0  1
0  0  0  392788  11032 235616  0  0  0  7  732 713 7  2 90 0  1
0  0  0  392788  11072 235576  0  0  0  4  678 710 9  2 88 0  1
1  0  0  392788  11112 236052  0  0  0  8  769 684 8  2 89 0  1
0  0  0  392788  11152 236012  0  0  0  3  672 703 7  2 90 0  1
0  0  0  392540  11192 235972  0  0  0  7  785 709 7  2 90 0  1
```

From Example 11-8, it appears that the system is stable and that there are no traces of swapping. As already recommended, we thought of cross-checking the utilization and other details from the z/VM level. Also, when things seem to be looking stable on Linux, but the problem is still occurring, it is better to gather information from the z/VM system for further investigation.

# ## 11.3 z/VM to the rescue

Even though we have many z/VM-based problem determination tools available, we directly started our investigation using the IBM z/VM Performance Toolkit,