
## 6.1.5 I/O 统计

关于存储设备的另一个信息来源是 DASD I/O 统计数据。通过 I/O 统计数据，可以收集并存储所有关于存储设备的重要信息到一个文件中，以便进一步分析。您可以根据需要开启或关闭 DASD I/O 统计数据。图 6-16 展示了如何开启和关闭 DASD I/O 统计数据。

![](img/f332344337ca8bf6846cb313a66ee0b3_238_0.png)

图 6-16 开启/关闭 DASD I/O 统计数据

若要重置收集过程，请将 DASD I/O 统计数据关闭后再重新开启。

有关 DASD I/O 统计数据的更多信息，另请参阅第 68 页的 3.1.8 节“netstat”。

## 6.2 案例研究

在本节中，我们将通过一个涉及实际问题的案例研究进行探讨。在这个案例研究中，我们讨论了一种场景，其中交换速率过高，导致系统吞吐量大幅下降。

我们有一个运行 DB2 数据库的 Linux 客户机系统。由于 DB2 请求的增加，Linux 系统的工作负载也随之增加。我们使用了 z/VM 工具和 Linux 基本工具来监控这种情况。在性能工具包窗口 FCX100 的第一页（图 6-17）中，系统的负载和分页活动均正常。

```
FCX100 CPU 2094 SER 2991E Interval 11:02:21 - 11:03:21 Perf. Monitor

CPU Load                                      Vector Facility Status or
PROC TYPE %CPU %CP %EMU %WT %SYS %SP %SIC %LOGLD %VTOT %VEMU REST ded. User
P00 CP 10 1 8 90 1 0 96 10 .. .. ... Master
P01 CP 10 1 9 90 0 0 96 10 .. .. ... Alternate
P02 CP 8 1 7 92 0 0 96 8 .. .. ... Alternate
P03 CP 8 1 7 92 0 0 96 8 .. .. ... Alternate

Total SSCH/RSC H 13/s Page rate 6.5/s Priv. instruct. 2266/s
Virtual I/O rate 14/s XSTORE paging 3.7/s Diagnose instr. 3/s
Total rel. SHARE 500 Tot. abs SHARE 0%

Queue Statistics: Q0 Q1 Q2 Q3 User Status:
VMDBKs in queue 0 1 0 6 # of logged on users 24
VMDBKs loading 0 0 0 0 # of dialed users 0
Eligible VMDBKs 0 0 0 0 # of active users 13
El. VMDBKs loading 0 0 0 0 # of in-queue users 7
Tot. WS (pages) 0 669 0 820955 % in-Q users in PGWAIT 0
Expansion factor 0 0 0 0 % in-Q users in IOWAIT 1
85% elapsed time 1.376 .172 1.376 8.256 % elig. (resource wait) 0

Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F12=Return
```

图 6-17 IBM z/VM 性能工具包显示正常的负载和分页活动

下一个窗口（图 6-18）显示了运行 DB2 工作负载的 Linux 客户机系统 LNXDB2 的详细视图。可以看到，在此阶段，I/O 速率相对较高，但未检测到问题。

```
FCX115 CPU 2094 SER 2991E Interval 10:08:37 - 10:08:38 Perf. Monitor

Detailed data for user LNXDB2
Total CPU : 2.5% Storage def. : 2048MB Page fault rate: .0/s
Superv. CPU : .3% Resident <2GB: 79391 Page read rate : .0/s
Emulat. CPU : 2.2% Resident >2GB: 37211 Page write rate: .0/s
VF total : ....% Proj. WSET : 168614 Pgs moved >2GB>: .0/s
VF overhead : ....% Reserved pgs : 0 Main > XSTORE : .0/s
VF emulation: ....% Locked pages : 5 XSTORE > main : .0/s
VF load rate: ..../s XSTORE dedic.: 0MB XSTORE > DASD : .0/s
I/O rate : 222/s XSTORE pages : 70160 SPOOL pg reads : .0/s
DASD I/O rate: .0/s DASD slots : 52619 SPOOL pg writes: .0/s
UR I/O rate : .0/s IUCV X-fer/s : .0/s MDC insert rate: .0/s
Diag. X'98' : .0/s Share : 100 MDC I/O avoided: .0/s
*BLOCKIO : .0/s Max. share : ...

#1/O active : 0 Active :100% PSW wait : 97% I/O act. : 0%
Stacked blk : .. Page wait : 0% CF wait : 0% Eligible : 0%
Stat.: EME,PO2,PSWT I/O wait : 0% Sim. wait: 1% Runnabl e : 1%

Proc. %CPU %CP %EM %VECT %VOHD %VEMU VLD/S IO/S Status
00 2.5 .3 2.2 .... .... .... .... 221 EME,PO2,PSWT
01 .0 .0 .0 .... .... .... .... .0 EME,PO2,PSWT

Data Space Name Size Mode PgRd/s PgWr/s XRd/s XWr/s Migr/s Steal/s
BASE 2048MB Priv .0 .0 .0 .0 .0 .0

Device activity and status:
0009 3215 .0 000C 254R CL *, EOF NOH NCNT

Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F12=Return
```

图 6-18 Linux 客户机系统的详细视图

在图 6-19（整体系统性能窗口的图像）中，我们可以看到 XSTORE 分页已经达到每秒 122 次。这表明存在严重的分页活动。

```
FCX100    CPU 2094  SER 2991E  Interval 10:07:21 - 10:08:21    Perf. Monitor

CPU Load                                 Vector Facility  Status or
PROC TYPE %CPU %CP %EMU %WT %SYS %SP %SIC %LOGLD %VTOT %VEMU REST ded. User
P00  CP   4    1   3  96   1   0   95     4      ..    ..    ... Master
P01  CP   4    1   3  96   0   0   94     4      ..    ..    ... Alternate
P02  CP   4    1   4  96   0   0   94     4      ..    ..    ... Alternate
P03  CP   4    1   4  96   0   0   94     4      ..    ..    ... Alternate

Total SSCH/RSCH   8/s      Page rate      14.4/s      Priv. instruct.  891/s
Virtual I/O rate  4/s      XSTORE paging  121.8/s    Diagnose instr.   6/s
Total rel. SHARE  400       Tot. abs SHARE 0%

Queue Statistics:   Q0    Q1    Q2    Q3    User Status:
VMDBKs in queue     0     0     0     6     # of logged on users      24
VMDBKs loading      0     0     0     0     # of dialed users         0
Eligible VMDBKs                0     0     0     # of active users        12
El. VMDBKs loading             0     0     0     # of in-queue users       6
Tot. WS (pages)     0     0     0 1007k   % in-Q users in PGWAIT    0
Expansion factor           0     0     0     % in-Q users in IOWAIT   0
85% elapsed time   1.656 .207 1.656 9.936   % elig. (resource wait)   0

Transactions        Q-Disp trivial non-trv   User Extremes:
Average users       .0     .0    .1     Max. CPU %   LNXWAS      6.4
Trans. per sec.     .8     1.7   .5     Max. VECT %  ........   .....
Av. time (sec)      .101   .017  .327   Max. IO/sec  LNXDB2      1.5
UP trans. time                 .017  .327   Max. PGS/s   LNXWAS      8.6
MP trans. time      .000   .000           Max. RESPG   LNXWAS    711653
System ITR (trans. per sec. tot. CPU) 20.2   Max. MDIO    ........   .....

Command ===>
F1=Help  F4=Top  F5=Bot  F7=Bkwd  F8=Fwd  F12=Return
```

图 6-19 严重的分页活动

几分钟后，我们看到 LNXDB2 Linux 客户机系统的 I/O 速率增加到每秒 583 次。

```
FCX115    CPU 2094  SER 2991E  Interval 10:12:27 - 10:12:28     Perf. Monitor

Detailed data for user LNXDB2

Total CPU   : 14.3%   Storage def. :   2048MB   Page fault rate:   .9/s
Superv. CPU :  1.4%   Resident <2GB:  77876   Page read rate :   .9/s
Emulat. CPU : 12.9%   Resident >2GB:  33658   Page write rate:   .0/s
VF total    : ....%   Proj. WSET   : 168614  Pgs moved >2GB:  .0/s
VF overhead : ....%   Reserved pgs :     0   Main > XSTORE :   .0/s
VF emulation: ....%   Locked pages :     5   XSTORE > main :   6.4/s
VF load rate: ..../s   XSTORE dedic. :    0MB   XSTORE > DASD :   .0/s
I/O rate    :  583/s   XSTORE pages :  75125   SPOOL pg reads :  .0/s
DASD I/O rate : .0/s   DASD slots   :  52754   SPOOL pg writes:  .0/s
UR I/O rate :  .0/s   IUCV X-fer/s  :   .0/s   MDC insert rate: .0/s
Diag. X'98' :  .0/s   Share        :   100   MDC I/O avoided:  .0/s
*BLOCKIO    :  .0/s   Max. share   :  ...

#I/O active :     0   Active     :100%   PSW wait : 97%   I/O act. : 0%
Stacked blk :  ...   Page wait   :  0%   CF wait  :  0%   Eligible : 0%
Stat.: EME,PO2,PSWT   I/O wait    :  0%   Sim. wait:  1%   Runnable : 2%

Proc.  %CPU  %CP  %EM  %VECT %VOHD %VEMU VLD/S IO/S  Status
00     13.6  1.4 12.2  ....  ....  ....  ....  577  EME,PO2,PSWT
01      .7  .0   .7  ....  ....  ....  ....   5.5  EME,PO2,PSWT

Data Space Name      Size Mode PgRd/s PgWr/s XRd/s XWr/s Migr/s Steal/s
BASE                  2048MB Priv   .9    .0    6.4   .0    .0     .0

Device activity and status:
0009 3215  .0           000C 254R      CL *, EOF   NOH NCNT

Command ===>
F1=Help  F4=Top  F5=Bot  F7=Bkwd  F8=Fwd  F12=Return
```

表 6-1 增加情况

```
FCX103    CPU 2094  SER 2991E  Interval 10:11:21 - 10:12:21    Perf. Monitor

Total DPA size            4'013MB          MDCACHE utilization:
Locked pages              14'984kB         Min. size in XSTORE            0kB
Trace table               ......kB         Max. size in XSTORE         1'024MB
Pageable                  3'999MB          Ideal size in XSTORE       314'688kB
Storage utilization       103%             Act. size in XSTORE       274'304kB
Tasks waiting for a frame 0               Bias for XSTORE                1.00
Tasks waiting for a page  1/s             Min. size in main stor.        0kB
                                          Max. size in main stor.     4'096MB
V=R area:                                 Ideal size in main stor.   277'676kB
Size defined              ...kB            Act. size in main stor.   176'692kB
FREE storage              ...kB            Bias for main stor.           1.00
V=R recovery area in use  ...%             MDCACHE limit / user      79'504kB
V=R user                  ........         Users with MDCACHE inserts      2
                                          MDISK cache read rate          0/s
Paging / spooling activity:               MDISK cache write rate       ...../s
Page moves <2GB for trans. 0/s            MDISK cache read hit rate     0/s
Fast path page-in rate    137/s            MDISK cache read hit ratio    71%
Long path page-in rate    2/s
Long path page-out rate   147/s
Page read rate            12/s             VDISKs:
Page write rate           9/s              System limit (blocks)      3882k
Page read blocking factor 23              User limit (blocks)        1005k
Page write blocking factor ...            Main store page frames         0
Migrate-out blocking factor 21            Expanded stor. pages          0
Paging SSCH rate          1/s             Pages on DASD              38680
SPOOL read rate           0/s
SPOOL write rate          0/s

Command ===>
F1=Help  F4=Top  F5=Bot  F7=Bkwd  F8=Fwd  F12=Return
```

表 6-2 XSTORE 持续急剧增加
