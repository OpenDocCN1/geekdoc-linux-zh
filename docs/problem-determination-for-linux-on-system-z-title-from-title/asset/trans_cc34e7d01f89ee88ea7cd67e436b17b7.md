
您需要的功能。进入报告后，许多报告都包含子菜单，或者通过将光标移至变量下方并按 Enter 键来实现进一步导航。实际上，许多报告包含多层导航，例如，您可以查看 DASD 卷的顺序列表并查看整体活动，此外还可以查看控制器功能。然后您可以深入查看，更详细地查看特定卷，再进一步深入查看微型磁盘设备活动。这种导航功能极大地促进了问题定位，由于增强了可访问性，使得对系统的整体理解（甚至深入到详细级别）变得更容易。各种数据报告分为通用系统数据、I/O 数据、历史数据和用户数据这几组。

初始菜单上未高亮显示的数字对应的性能屏幕项目无法选择，因为尚未收集这些项目的 CP 监控数据。可能的原因包括：

-   所需的监控记录不可用，因为您的 VM 系统的 CP 级别尚未生成它们。
-   所需的监控域尚未启用。
-   第一个监控采样区间尚未结束，我们仍在等待初始的监控记录集。
-   该显示用于无法在该系统上生成的数据（例如，在未分区系统上的 LPAR 数据）。

### 2.2.2 选择性能屏幕

屏幕被分组为通用系统数据、I/O 数据、用户数据（显示上一个监控采样区间或整体平均值的数据），以及一系列按时间记录的文件，它们显示每个监控采样区间的单独值集。可以通过执行以下操作之一从初始菜单中选择它们：

-   在命令线输入所选性能数据（显示在命令线上）的编号
-   将光标移动到所选显示项（请注意，如果使用制表键，它只会移动到高亮显示的编号）
-   输入所需屏幕的 `short-path` 命令

然后按 Enter 键。

为了获取用于问题定位的有意义数据，您需要了解在性能工具包中从哪里获取这些数据。

收集系统当前状态信息的一个良好起点是通用系统数据类别中的屏幕。从第一个选项开始，我们开始进行系统性能健康检查。选择 1 并按 Enter，或将光标置于屏幕上的适当字段并按 Enter。此选项显示整体处理器利用率、系统争用以及用户群信息。用户数据包括用户总数、活动用户数以及正在等待资源（如存储页或 I/O）的用户数。

显示的屏幕如图 2-17 所示。

```text
FCX100 CPU 2094 SER 7991E Interval 11:27:27 - 11:28:27 Perf. Monitor
CPU Load Vector Facility Status or
PROC TYPE %CPU %CP %EMU %WT %SYS %SP %SIC %LOGLD %VTOT %VEMU REST ded. User
P00 CP 12 1 12 88 1 0 92 12 .. .. ... Master
P01 CP 29 0 29 71 0 0 81 29 .. .. ... Alternate
P02 CP 34 0 34 66 0 0 87 34 .. .. ... Alternate
P03 CP 23 0 23 77 0 0 81 23 .. .. ... Alternate

Total SSCH/RSCH 122/s Page rate 9.6/s Priv. instruct. 263/s
Virtual I/O rate 116/s XSTORE paging 804.9/s Diagnose instr. 1/s
Total rel. SHARE 700 Tot. abs SHARE 0%

Queue Statistics: Q0 Q1 Q2 Q3 User Status:
VMDBKs in queue 0 0 1 6 # of logged on users 25
VMDBKs loading 0 0 0 0 # of dialed users 0
Eligible VMDBKs 0 0 0 0 # of active users 11
El. VMDBKs loading 0 0 0 0 # of in-queue users 7
Tot. WS (pages) 0 0 871 1653k % in-Q users in PGWAIT 0
Expansion factor 0 0 0 0 % in-Q users in IOWAIT 0
85% elapsed time 4.712 .589 4.712 28.27 % elig. (resource wait) 0

Transactions Q-Disp trivial non-trv User Extremes:
Average users .2 .1 .3 Max. CPU % LXOR4 95.1
Trans. per sec. .7 .6 .1 Max. VECT % ....... .....
Av. time (sec) .307 .258 3.061 Max. IO/sec LXOR4 113
UP trans. time .258 3.061 Max. PGS/s LXOR4 9.6
MP trans. time .000 .000 Max. RESPG LXORINST 511413
System ITR (trans. per sec. tot. CPU) 1.4 Max. MDIO LXOR4 1.9

Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F12=Return
```

图 2-17 IBM z/VM 性能工具包屏幕 1，CPU 负载和事务 FCX100

根据从第一个屏幕获得的结果，我们现在可以查看 IBM z/VM 性能工具包菜单的其他区域，收集用于问题定位的信息。例如，若要获取有关每个用户 ID 处理器资源消耗的更多信息，我们显示 21- 用户资源使用页面。此显示如图 2-18 所示。

```text
FCX112    CPU 2094  SER 7991E  Interval 11:26:27 - 11:27:27    Perf. Monitor
------    ---- ---- ----    -------- --------    ------------
<---- CPU Load ----> <---- Virtual IO/s ---->
<--Seconds--> T/V
Userid    %CPU TCPU VCPU Ratio Total DASD Avoid Diag98 UR Pg/s User Status
>>Mean>>  3.87 2.321 2.298 1.0 7.7 7.7 .3 .0 .0 .1 ---,---,---
DISKACNT  0.0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
DTCVSW1  .00 .000 .000 ... .0 .0 .0 .0 .0 .0 ESA,---,DOR
DTCVSW2  .00 .000 .000 ... .0 .0 .0 .0 .0 .0 ESA,---,DOR
EREP     0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
FTPSERVE 0 0 0 ... 0 0 0 0 0 0 XC,---,DOR
LNXINST  .03 .016 .015 1.1 .0 .0 .0 .0 .0 .0 EME,CL1,DIS
LNXMAINT 0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
LXORINST .40 .239 .222 1.1 .4 .4 .0 .0 .0 .0 EME,CL2,DIS
LXORI    .18 .107 .093 1.2 .0 .0 .0 .0 .0 .0 EME,CL3,DIS
LXOR3    .18 .108 .100 1.1 1.1 1.0 .0 .0 .0 .0 EME,CL3,DIS
LXOR4    94.1 56.43 56.01 1.0 181 181 1.0 .0 .0 2.6 EME,CL3,DIS
MAINT    0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
OPERATOR 0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
OPERSYMP 0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
PERFSVM  .01 .005 .004 1.3 .2 .2 .1 .0 .0 .1 ESA,---,DOR
TCPIP    .01 .003 .002 1.5 .0 .0 .0 .0 .0 .0 ESA,---,DOR
TCPMAINT 0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
TEACHOR1 .69 .416 .379 1.1 9.5 9.5 5.8 .0 .0 .0 EME,CL3,DIS
TEACHOR2 1.16 .694 .634 1.1 .5 .5 .0 .0 .0 .0 EME,CL3,DIS
USER1    0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
USER10   0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
USER15   0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
VMSERVR  0 0 0 ... 0 0 0 0 0 0 ESA,---,DOR
Select a user for user details or IDLEUSER for a list of idle users
Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F10=Left F11=Right F12=Return
```

图 2-18 性能工具包屏幕 21，用户资源使用 FCX112

例如，如果一个 Linux 系统消耗了大量 CPU 资源，我们可以深入查看并显示有关此特定用户 ID 的更详细信息。为此，请将光标放置在您想要获取更多信息的用户 ID 上，并按 Enter。在我们的示例中，我们想要获取更多关于用户 ID LXOR4 的信息。出现的屏幕如图 47 页的图 2-19 所示。

### FCX115 CPU 2094 SER 7991E 区间 11:44:02 - 11:44:37 性能监控器

用户 LXOR4 的详细数据

```text
Total CPU : 93.5% Storage def. : 2200MB Page fault rate: 1.8/s
Superv. CPU : 1.7% Resident <2GB: 105456 Page read rate: 16.5/s
Emulat. CPU : 91.8% Resident >2GB: 424406 Page write rate: .1/s
VF total : .....% Proj. WSET : 544391 Pgs moved >2GB>: .0/s
VF overhead : .....% Reserved pgs : 0 Main > XSTORE : 99.9/s
VF emulation: .....% Locked pages : 6 XSTORE > main : 15.1/s
VF load rate: ..../s XSTORE dedic.: OMB XSTORE > DASD : .1/s
I/O rate : 410/s XSTORE pages : 16362 SPOOL pg reads : .1/s
DASD I/O rate: 406/s DASD slots : 22663 SPOOL pg writes: .0/s
UR I/O rate : .0/s IUCV X-fer/s : .0/s MDC insert rate: 344/s
Diag. X'98' : .0/s Share : 100 MDC I/O avoided: 81.4/s
*BLOCKIO : .0/s Max. share : ....
#I/O active : 0 Active :100% PSW wait : 0% I/O act. : 29%
Stacked blk : .. Page wait : 7% CF wait : 0% Eligible : 0%
Stat.: EME,DSC,RNBL I/O wait : 7% Sim. wait: 0% Runnabl e: 86%
Data Space Name Size Mode PgRd/s PgWr/s XRd/s XWr/s Migr/s Steal/s
BASE 2200MB Priv 16.5 .1 15.1 99.9 .1 101
Device activity and status:
0009 3215 .0 000C 254R CL *, EOF NOH NCNT
000D 254P CL A, CO 01, NOH NCNT 000E 1403 CL A, CO 01, NOH NCNT
0190 .0 CF31,RR, 107Cyl,---->0 0191 .0 CF37,WR, 10Cyl,---->0
019D .0 CF34,RR, 146Cyl,---->0 019E .0 CF34,RR, 250Cyl,---->0
0200 3390 .0 8025,WR,3338Cyl,RS/RL 0201 .7 D437,WR,10016Cy,RS/RL
0300 .4 D438,WR,10016Cy,RS/RL 0301 1.0 D439,WR,10016Cy,RS/RL
0302 .0 D43A,WR,10016Cy,RS/RL 0400 403 D43B,WR, 20% MDC eff.
0401 1.3 DB10,WR,3336Cyl,---->2 0402 .0 CF34,RR, 146Cyl,---->0
0405 .0 CF34,RR, 156Cyl,---->0 0500 .0 DA11,WR, 450Cyl,RS/RL
0501 .0 DA11,WR, 450Cyl,RS/RL 0502 .0 DA11,WR, 450Cyl,RS/RL
0503 .0 DA11,WR, 450Cyl,RS/RL 0504 .0 DA11,WR, 450Cyl,RS/RL
0600 OSA .0 QDIO->TEACHOR1 QDIO 0601 OSA .0 QDIO->TEACHOR1 QDIO
0602 OSA 3.5 QDIO->TEACHOR1 QDIO 0650 OSA .0 QDIO->LXOR3 QDIO
0651 OSA .0 QDIO->LXOR3 QDIO 0652 OSA .0 QDIO->LXOR3 QDIO
0700 .0 D436,WR,10016Cy,RS/RL 0701 .0 DA14,WR,3338Cyl,RS/RL
0800 .0 DA12,WR,1500Cyl,RS/RL 0900 .0 DB12,WR,10016Cy,>4886
0901 .0 DB13,RR,10016Cy,---->0 0902 .0 DB14,RR,10016Cy,>1979
Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F12=Return
```

图 2-19 用户 ID LXOR4 的详细数据，屏幕 FCX115

