
```
martyp $ timex listing

real        0.02
user        0.00
sys         0.02

martyp $ timex -s listing

real        0.02
user        0.00
sys         0.01

SunOS 5.7 Generic sun4m     08/21

07:48:30  %usr    %sys    %wio    %idle
07:48:31  32      68      0       0

07:48:30 bread/s read/s %rcache bwrIit/s lwrit/s %wcache pread/s pwrit/s
07:48:31  0       0      100     0       0       100     0       0
Average 0       0      100     0       0       100     0       0

07:48:30 device    %busy avque r+w/s blks/s await avserv
07:48:31 fd0       0       0.0   0       0       0.0     0.0
         nfs1      0       0.0   0       0       0.0     0.0
         nfs219    0       0.0   0       0       0.0     0.0
         sdd1      0       0.0   0       0       0.0     0.0
         sdd1_a    0       0.0   0       0       0.0     0.0
         sdd1_b    0       0.0   0       0       0.0     0.0
         sdd1_c    0       0.0   0       0       0.0     0.0
         sdd1_g    0       0.0   0       0       0.0     0.0
         sdd3      0       0.0   0       0       0.0     0.0
         sdd3_a    0       0.0   0       0       0.0     0.0
         sdd3_b    0       0.0   0       0       0.0     0.0
         sdd3_c    0       0.0   0       0       0.0     0.0
         sdd6      0       0.0   0       0       0.0     0.0
Average  fd0       0       0.0   0       0       0.0     0.0
         nfs1      0       0.0   0       0       0.0     0.0
         nfs219    0       0.0   0       0       0.0     0.0
         sdd1      0       0.0   0       0       0.0     0.0
         sdd1_a    0       0.0   0       0       0.0     0.0
         sdd1_b    0       0.0   0       0       0.0     0.0
         sdd1_c    0       0.0   0       0       0.0     0.0
         sdd1_g    0       0.0   0       0       0.0     0.0
         sdd3      0       0.0   0       0       0.0     0.0
         sdd3_a    0       0.0   0       0       0.0     0.0
         sdd3_b    0       0.0   0       0       0.0     0.0
         sdd3_c    0       0.0   0       0       0.0     0.0
         sdd6      0       0.0   0       0       0.0     0.0

07:48:30 rawch/s canch/s outh/s rcvin/s xmtin/s mdmin/s
07:48:31 0       0       147    0       0       0
Average  0       0       147    0       0       0

07:48:30 scal/s sread/s swrit/s fork/s exec/s rchar/s wchar/s
07:48:31 2637   0       95     15.79  15.79  0      19216
Average  2637   0       95     15.79  15.79  0      19216

07:48:30 swpin/s bswin/s swpot/s bswopt/s pswch/s
07:48:31 0.00    0.0    0.00   0.0    116
Average  0.00    0.0    0.00   0.0    116

07:48:30 iget/s namei/s dirbk/s
07:48:31 0      195    121
Average  0      195    121

07:48:30 runq-sz #runocc swpg-sz #swpocc
07:48:31 2.0      526
Average  2.0      526

07:48:30 proc-sz ov inod-sz ov file-sz ov lock-sz
07:48:31 45/986   0   973/4508 0   357/357 0   0/0
Average  45/986   0   973/4508 0   357/357 0   0/0

07:48:30 mag/s sema/s
07:48:31 0.00  0.00
Average  0.00  0.00

07:48:30 atch/s pgin/s ppgin/s pfilt/s vflt/s slock/s
07:48:31 0.00   0.00   0.00   505.26  1036.84 0.00
Average  0.00   0.00   0.00   505.26  1036.84 0.00

07:48:30 pgout/s ppgout/s pgfree/s pgscan/s #ufs_ipf
07:48:31 0.00    0.00    0.00    0.00     0.00
Average  0.00    0.00    0.00    0.00     0.00

07:48:30 freemem freeswap
07:48:31 15084   1224421
Average  15084   1224421

07:48:30 sm1_mem alloc fail lg_mem alloc fail ovsz_alloc_fail
07:48:31 2617344 1874368 0 17190912 10945416 0 3067904 0
Average  186953 133883 0 1227922 781815 0 219136 0
```

### 更高级和图形化的性能工具

在操作 UNIX 时，命令行是一种生活方式。UNIX 起源于命令行，并且至今仍主要基于命令行。尽管在发出命令时需要了解很多知识，尤其是在涉及系统性能时，但你通过刚刚介绍的许多命令可以非常快速地进行深入挖掘。

大多数 UNIX 变体都允许用户购买图形化性能工具。一些系统也附带了基本的图形化性能工具。通常，如果您想要执行高级性能分析，最终会购买高级性能分析工具。我们将在后续章节中快速浏览几款性能工具。

图 13-1 展示了 Red Hat Linux 系统附带的三种性能工具，我在本章的许多示例中都使用了该系统。

![](img/75f39fc91296b889c0653851accdfd46_920_0.png)

*系统监视器 (`gtop`)* 窗口，带有显示 *CPU*、*MEM*、*SW* 和 *LA* 的条形图，单个进程信息以及其他有用的性能数据。

*`top`* 窗口，带有负载平均值、每个状态的进程数、处理器状态的时间百分比、单个进程相关信息以及其他有用的性能数据。
