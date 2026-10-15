
### FCX100 CPU 2094 SER 2991E Interval 11:02:21 - 11:03:21 Perf. Monitor

```
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

下一个窗口（图 6-18）显示了运行 DB2 工作负载的 Linux 客户机系统 `LNXDB2` 的详细视图。可以看到，在此阶段，I/O 速率相对较高，但未检测到问题。

### FCX115 CPU 2094 SER 2991E Interval 10:08:37 - 10:08:38 Perf. Monitor

```
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

在图 6-19（整体系统性能窗口的图像）中，我们可以看到 `XSTORE` 分页已经达到每秒 122 次。这表明存在严重的分页活动。
