
Statspack 和 Oracle Enterprise Manager（也称为 Grid Control）；以及诸如 sar、vmstat 和 iostat 之类的操作系统工具。

### sar

系统活动报告程序（sar）对于总体监控系统性能非常有用。使用 sar，你可以监控 CPU 利用率、内存和网络接口。sar 不擅长的一点是监控 I/O 子系统。sar 提供了许多不同的选项，具体取决于你想要监控系统的哪些内容以及如何监控。

不带参数运行 sar 会显示过去 24 小时的 CPU 利用率，如下所示：

```
Linux 2.4.21-15.EL (ptc6)            09/28/2004

12:00:00 AM CPU  %user  %nice %system %idle
12:10:00 AM all  1.13   0.00   0.13    98.74

11:40:00 AM all  4.01   0.00   3.80    92.18
Average: .    all  3.67   0.01   4.58    91.74
```

此信息通过 crontab 进程自动保存。使用 -A 参数运行 sar 会显示过去 24 小时关于系统的更多信息。由于数据量庞大，这里不予展示。此外，可以使用 sar -n DEV 命令监控网络接口。

```
[root@ptc6 root]# sar -n DEV
Linux 2.4.21-15.EL (ptc6)             09/28/2004

12:00:00 AM IFACE  rxpck/s  txpck/s  rxby/s  txby/s  rxcmp/s  txcmp/s  rxmcst/s
12:10:00 AM lo     3.56     3.56   286.63  286.63    0.00     0.00     0.00
0.00
12:10:00 AM eth0   0.00     0.00     0.00    0.00     0.00     0.00     0.00
0.00

11:40:00 AM lo     3.63     3.63   295.64  295.64    0.00     0.00     0.00
0.00
11:40:00 AM eth0   0.00     0.00     0.00     0.00     0.00     0.00     0.00
0.00
Average:  . lo     4.08     4.08   330.71  330.71    0.00     0.00     0.00
0.00
Average:  . eth0   0.00     0.00     0.00    0.00     0.00     0.00     0.00
0.00
```

此外，根据你正在调试的内容，还有许多其他 sar 参数可能很有用。

### vmstat

vmstat 命令提供有关进程、内存、分页等的信息。
该命令是确定是否存在可用内存以及有多少内存的好地方，同时还提供有关进程和分页的信息，如下所示：

```
[root@ptc6 root]# vmstat

               swap          io             cpu
procs  r  b   swpd  free  buff  cache si so  bi  bo in  cs us sy id wa
      0  0  133008  9248 122396 274436  0  2   8  128  208 282 2 3 85 10
```

### top

top 工具用于获取系统活动的整体视图。top 会持续显示运行最频繁的进程以及系统的整体视图，如下所示：

```
11:59:07  up  19:14,   5 users,   load average: 0.26, 0.21, 0.18
121 processes:  120 sleeping, 1 running, 0 zombie, 0 stopped
CPU states:  cpu    user    nice system   irq softirq  iowait    idle
             total    6.7%    0.0%    3.8%    0.9%     0.0%    6.7%    81.5%
Mem:   512480k total,    50442k used,    8068k free,     0k shrd,  122415k buff
        354344k actv,   86452k in-w,   9504k in-c       0 iniT
Swap:  5632192k av,    133008k used,  5499184k free     27600k cached
PID   USER    PR    NI  SIZE    RSS SHRE STAT %CPU %MEM TIME COMMAND
4991 root      15    0    79560  3032 1868 S       1.9  0.2    0:00 /usr/X11R6/bin/X
0 root        0     0       0     0    0    SW      0.0  0.0    0:00 top
8358 root      20    0   1176  1176  892 R       2.9  0.2    0:00 o_top_c
5292 oracle   15    0   26272  12M 9312 S       1.9  2.4   21:21 o_ora_arc1_orcl
8061 oracle   15    0   1196  1196  904 S       1.9  0.2    0:10 o_Top
5290 oracle   15    0   26232  10M 9200 S       0.9  2.0   21:35 o_ora_arc0_orcl
1 root        15    0    508   480  448 S       0.0  0.0    0:04 o_init
2 root        15    0      0     0    0    SW      0.0  0.0    0:00 o_keventd
3 root        15    0      0     0    0    SW      0.0  0.0    0:00 o_kapped
4 root        34   19      0     0    0    SW      0.0  0.0    0:00 o_ksctirqd/0
7 root        25    0      0     0    0    SW      0.0  0.0    0:00 o_kifluan
5 root        15    0      0     0    0    SW      0.0  0.0    0:01 o_kswapd
6 root        15    0      0     0    0    SW      0.0  0.0    0:00 o_kscand
8 root        15    0      0     0    0    SW      0.0  0.0    0:00 o_kupdatad
9 root        25    0      0     0    0    SW      0.0  0.0    0:00 o_ksoftirqd
15 root      15    0      0     0    0    SW      0.0  0.0    0:00 o_shc_dv_0
16 root      25    0      0     0    0    SW      0.0  0.0    0:00 o_esci_gh_0
19 root      15    0      0     0    0    SW      0.0  0.0    0:00 o_jxksunald
90 root      25    0      0     0    0    SW      0.0  0.0    0:00 o_kibhid
1669 root    15    0      0     0    0    SW      0.0  0.0    0:00 o_kifluan
4052 root    15    0    620  580  536 S       0.0  0.1    0:00 o_asylogd-x 0
4056 root    15    0   452   396  392 S       0.0  0.0    0:00 o_klogd -x
4084 rpc     15    0   556  484  480 S       0.0  0.0    0:00 o_portmap
4104 spucser 15    0   556  616  612 S       0.0  0.0    0:00 o_psp_statd
4118 root    RT    0   556  448  420 S       0.0  0.0    0:00 /sbin/auditd
4173 root      24  0  508  460  456 S   0.0   0.0   0:00  0 /usr/sbin/spamd -p
10 -w 5 -M -P /etc/sysa
4257 root      15  0 1252 1140 1000 S   0.0   0.2   0:00  0 /usr/sbin/selhd
4273 root      17  0  856  812  732 S   0.0   0.1   0:00  0 xinetd -stayalive
-pidfile /var/run/xine
4602 root      15  0 1720  856  812 S   0.0   0.1   0:00  0 vmcd
4607 root      15  0 2944 1260 888 S   0.0   0.2   0:00  0
/usr/openv/netbackup/bin/bprd
4639 root      15  0 2468 1036 824 S   0.0   0.2   0:00  0
/usr/openv/netbackup/bin/bpdnm
```

我总是使用 -c 参数调用 top，它会显示命令行而不是仅显示正在运行的命令。这在监控系统时提供了更详细的信息。

### iostat

在监控系统时，可能最重要的工具之一是 iostat，它显示有关 I/O 子系统的信息，例如每秒读/写次数、每秒写入块数、等待时间和响应时间。你可以使用 -x 限定符调用 iostat 以获取详细的 I/O 信息，如下所示：

```
[root@ptc6 root]# iostat -x
Linux 2.4.21-15.EL (ptc6)           09/28/2004
avg-cpu:  %user   %nice  %sys  %idle
      2.49    0.01   2.73   94.76
Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s  wsec/s      rkB/s     wkB/s  avgqu-sz   %util
avgrq-sz    await     svctm     %util
/dev/hda0        1.35  272.29   1.01  111.25  18.75  3068.59      9.38  1534.30     27.50
   6.17     1.95     3.80    42.67
/dev/hda1        0.00     0.00   0.00     0.00     0.00     0.00      0.00      0.00      0.26
   0.00    33.38    26.62
/dev/hda2        0.00     0.53   0.11     0.07     0.88     4.77      0.44      2.38     31.86
   0.16    31.85    34.08      0.60
/dev/hda3        1.34  271.76   0.90  111.18  17.85  3063.83      8.93  1531.91     27.50
   2.03     1.81     1.07    12.02
/dev/hdb0        0.00     0.00   0.00     0.00     0.01     0.00      0.00      0.00     11.49
   5.44     7.66  4383.47     42.67
/dev/hdb1        0.00     0.00   0.00     0.00     0.00     0.00      0.00      0.00     13.05
   0.00     3.16     3.16
/dev/hdb2        0.00     0.00   0.00     0.00     0.00     0.00      0.00      0.00     13.05
   0.00     8.95     8.95
```

iostat 命令是我在监控系统时最常用的工具之一，因为 I/O 通常是问题所在。本工具和其他工具将在第 15 章中讨论，我们在其中研究系统硬件的性能调优。

## Upgrading the Linux Operating System

升级 Linux 操作系统是必须非常谨慎的操作。我不建议使用 *up2date*（红帽）或 YaST（SUSE）自动更新系统，因为可能出现问题。Oracle 系统有一套特定的要求，你在前几章中已经看到过。Oracle 系统依赖于特定版本的 *gcc*、*libstdc*、*openmotif*、*make*、*binutils* 和 Java 运行时环境。当你自动更新系统时，其中许多组件也可能被更新。这可能会或可能不会导致 Oracle 系统出现问题。因此，如果你自动更新系统，则风险自负。

让我们看看作为 Oracle DBA 你需要完成的某些 Oracle 任务。

## Starting Up the Instance

启动实例

最基本的数据库管理任务之一是启动和关闭实例。听起来很简单，但根据情况的不同，完全启动或打开 Oracle 数据库有多种方法。如果我们想启动并打开数据库，那么只需通过 *sqlplus* 使用具有 *sysdba* 或 *sysoper* 系统权限的用户对数据库进行身份验证，然后发出 startup 命令即可。

```
sqlplus
SQL*Plus: Release 10.1.0.2.0 - Production on Mon Jun 21 18:55:06 2004

Copyright (c) 1982, 2004, Oracle. All rights reserved.

Enter user-name: sys as sysdba
Enter password:
Connected to an idle instance.

SQL> startup
ORACLE instance started.

Total System Global Area 188743680 bytes
Fixed Size 778036 bytes
Variable Size 162537676 bytes
Database Buffers 25165824 bytes
Redo Buffers 262144 bytes
Database mounted.
Database opened.

SQL>
```
