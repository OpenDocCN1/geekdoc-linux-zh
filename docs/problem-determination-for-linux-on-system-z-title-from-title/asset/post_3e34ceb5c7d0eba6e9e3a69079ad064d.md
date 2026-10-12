
Now the XSTOR paging increased dramatically to 1556 per second. This means that the overall system throughput is very low since the system is short on memory, and therefore the paging activity is very high.

```
FCX100 CPU 2094 SER 2991E Interval 10:14:21 - 10:15:21 Perf. Monitor

PROC TYPE %CPU %CP %EMU %WT %SYS %SP %SIC %LOGLD %VTOT %VEMU REST ded. User
P00 CP 9 2 7 91 1 0 95 9 .. .. ... Master
P01 CP 7 1 6 93 0 0 96 7 .. .. ... Alternate
P02 CP 7 1 6 93 0 0 96 7 .. .. ... Alternate
P03 CP 11 1 10 89 0 0 95 11 .. .. ... Alternate

Total SSCH/RSCH 12/s Page rate 51.6/s Priv. instruct. 1856/s
Virtual I/O rate 7/s XSTORE paging 1556/s Diagnose instr. 28/s
Total rel. SHARE 500 Tot. abs SHARE 5%

Queue Statistics: Q0 Q1 Q2 Q3 User Status:
VMDBKs in queue 1 1 0 6 # of logged on users 24
VMDBKs loading 0 0 0 0 # of dialed users 0
Eligible VMDBKs 0 0 0 0 # of active users 12
El. VMDBKs loading 0 0 0 0 # of in-queue users 8
Tot. WS (pages) 119 530 0 987786 % in-Q users in PGWAIT 0
Expansion factor 0 0 0 0 % in-Q users in IOWAIT 0
85% elapsed time 1.528 .191 1.528 9.168 % elig. (resource wait) 0

Transactions Q-Disp trivial non-trv User Extremes:
Average users .1 .0 .1 Max. CPU % LNXWAS 16.9
Trans. per sec. 1.4 1.9 .5 Max. VECT % ....... .....
Av. time (sec) .088 .014 .222 Max. IO/sec LNXWAS 1.6
UP trans. time .014 .222 Max. PGS/s LNXSU3 29.7
MP trans. time .000 .000 Max. RESPG LNXWAS 763955
System ITR (trans. per sec. tot. CPU) 12.9 Max. MDC10 ....... .....
Emul. ITR (trans. per sec. emul. CPU) .0 Max. XSTORE LNXDB2 95945

Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F12=Return
```

Table 6-3 The ninth column from the left shows the emergency scanning rates

As a result of this high workload, shortage of memory, and extremely high paging activity, the system is in a so-called emergency scanning mode. This can be seen in Table 6-4 on page 230. See the ESCN field, which indicates that the system is short on memory and looking for free pages.

Emergency scanning is an indicator that the system is critically short of storage for some reason. When short of storage pages, the system begins a three-level scanning process: scan 1, scan 2, and then the most serious, emergency scanning. The system is being reduced to extreme measures while hunting for main storage pages, and the situation is so severe that it will steal them from any user. Ultimately, whether they are inactive, in queue, or active, it eventually even steals pages from shared segments and the CP system process.

```
FCX101    CPU 2094  SER 2991E  Interval 07:44:00 - 10:16:21    Perf. Monitor
TIME > PPAG %ST ALO/S FPGS %FR SHAR #TW ESCN %PGSL %SPSL XSTAV %XS XAL/S XAG
09:51 1000k 108 134 ... 0 95k 5 77 13 66 1024M 97 228 21
09:52 1000k 18 420 ... 0 93k 2 99 14 66 1024M 99 1309 28s
09:53 1000k 30 52 ... 0 94k 0 100 14 66 1024M 99 163 43-
09:54 1000k 102 130 ... 0 94k 0 94 14 66 1024M 99 420 48R
09:55 1000k 103 223 ... 0 94k 0 95 14 66 1024M 99 666 35R
09:56 1000k 103 46 ... 0 95k 0 100 14 66 1024M 99 133 53R
09:57 1000k 103 28 ... 0 96k 0 80 14 66 1024M 99 82 80R
09:58 1000k 103 15 ... 0 96k 0 100 14 66 1024M 99 59 123R
09:59 1000k 103 10 ... 0 96k 0 50 14 66 1024M 99 34 188R
10:00 1000k 103 16 ... 0 96k 0 100 14 66 1024M 99 49 239R
10:01 1000k 103 25 ... 0 96k 0 100 14 66 1024M 99 82 252R
10:02 1000k 103 18 ... 0 96k 0 100 15 66 1024M 99 66 252S
10:03 1000k 103 30 ... 0 96k 1 57 15 66 1024M 99 101 216S
10:04 1000k 103 12 ... 0 96k 0 50 15 66 1024M 99 31 313S
10:05 1000k 103 7 ... 0 96k 0 0 15 66 1024M 99 55 507R
10:06 1000k 103 25 ... 0 96k 0 100 15 66 1024M 98 41 456S
10:07 1000k 102 19 ... 0 97k 1 100 15 66 1024M 99 61 454S
10:08 1000k 102 21 ... 0 97k 1 100 15 66 1024M 99 70 313R
10:09 1000k 102 20 ... 0 97k 2 75 15 66 1024M 99 51 341R
10:10 1000k 103 22 ... 0 97k 1 100 15 66 1024M 99 83 309R
10:11 1000k 103 31 ... 0 97k 1 88 15 66 1024M 99 96 259R
10:12 1000k 103 50 ... 0 97k 1 100 15 66 1024M 99 150 199R
10:13 1000k 104 251 ... 0 96k 1 91 15 66 1024M 99 596 65R
10:14 1000k 106 369 ... 0 95k 0 98 14 66 1024M 99 1067 32S
10:15 1000k 100 295 ... 0 95k 3 98 14 66 1024M 99 819 25R
10:16 1000k 100 57 ... 0 96k 0 100 14 66 1024M 99 95 40R
Enter 'GRAPHICs' command for history graphics selection menu
Command ===>
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F10=Left F11=Right F12=Return
```

Table 6-4 Summary of memory usage of user IDs on the z/VM system

> **Note:** See also Chapter 11, “Case study: slow responding Web site” on page 313, for more information about emergency scanning.

In the last window you see a summary of the memory usage of user IDs on the z/VM system. You see that our Linux running the DB2 workload has a lot of memory allocated and uses the most XSTORE pages (Table 6-5).

```
FCX113 CPU 2094 SER 2991E Interval 10:17:21 - 10:18:21 Perf. Monitor  
> . > . . . . . .  
Data >---------- Number of Pages ---------->  
Spaces > >-Resident-> <<-Locked-->  
Userid Owned >Resrwd R>2GB R>2GB L<2GB L>2GB XSTOR DASD Stor Nr of  
>System< .0 > 0 21096 19298 0 12 7778 9617 299M Users 24  
COSTA .0 > 0 0 0 0 176 0 32M  
DATAMOVE 0 > 0 0 0 0 228 391 32M  
DIRMAINT 0 > 0 0 0 0 405 1605 32M  
DISKACNT 0 > 0 0 0 0 2252 32M  
DTCVSW1 0 > 0 1 28 1 0 20 2544 32M  
DTCVSW2 0 > 0 29 28 29 5 256 2517 32M  
ERE P 0 > 0 0 0 0 0 1233 32M  
GCS 0 > 0 1 0 1 0 52 16M  
LNXDB2 0 > 0 64606 24293 5 9 96169 52155 2048M  
LN X IHS 0 > 0 37057 61381 42 44 21793 10563 512M  
LN XSU1 0 > 0 5762 8059 6 4 36900 88499 512M  
LN XSU3 0 > 0 1437 1220 7 6 6915 9003 64M  
LN XSU4 0 > 0 489 440 102 156 65 44272 256M  
LN XWAS 0 > 0 394602 367234 8 5 21001 3012 3072M  
MAINT 0 > 0 0 0 0 0 1401 128M  
OPERATOR 0 > 0 0 0 0 0 0 32M  
OPERSYMP 0 > 0 0 0 0 0 1267 32M  
PERF36 0 > 0 45 354 0 0 2507 3236 64M  
PWM 0 > 0 2 1 2 1 70 304 32M  
RS CS 0 > 0 2 36 1 0 0 1218 32M  
TCP IP 0 > 0 470 72 327 52 151 2568 32M  
WMSERV R 0 > 0 1 0 1 0 2 1192 32M  
WMSERV S 0 > 0 1 0 1 0 2 1337 64M  
Select a user for user details  
Command ===>  
F1=Help F4=Top F5=Bot F7=Bkwd F8=Fwd F10=Left F11=Right F12=Return
```

Table 6-5 Linux running DB2 workload has a lot of memory allocated and uses the most XSTORE pages

**Note:** You can also use the **Toolkit → Quick Access Menu** to issue the **Toolkit → RXFM → Insert_tool** commands.

![](img/f332344337ca8bf6846cb313a66ee0b3_248_0.png)

## Eligibility lists

This chapter discusses the CP scheduling process and z/VM tools for problem determination. We also discuss the corrective measures that we need to take to overcome the problem with respect to the eligibility lists.

### 7.1 CP scheduler

When you log on to z/VM, CP creates a control block that is the anchor for a large amount of information about your virtual machine. This block is called a Virtual Machine Descriptor Block (VMDBK). It is pointers to this block that get moved around the different lists.

![](img/f332344337ca8bf6846cb313a66ee0b3_249_0.png)

Figure 7-1 z/VM Scheduler lists

Each user is in one of the following lists:

- Dispatch list (D-list) - users ready (near-ready) to run
- Eligible list (E-list) - "Time Out" chair for users that want to be in dispatch list.
- Dormant list - users who are idle (as far as we know)

If your virtual machine is not doing anything, then CP places it in the dormant list, which implies that your virtual machine is asleep. If you wake it up (for instance, by pressing the Enter key on your console), it will get moved to the eligible list, where it is eligible to receive system resources. Before it is given any resources, however, the virtual machine is examined by the scheduler. The scheduler looks in the VMDBK of your virtual machine to see what resources you have used in the past. Processor, storage, and paging are some of the resources examined.

If you have just logged on, there will not be much information in the VMDBK, so the scheduler thinks of you as an interactive user, also known as a class 1 user. A class 1 user is normally a CMS interactive user or a very lightly loaded guest operating system. When the scheduler determines that there is enough resource available to satisfy your needs without putting any other users in jeopardy, you will be moved to the dispatch list, where you wait in turn for your allowance of CPU time (time slice). When your turn arrives, your virtual machine is run on an available processor.

The time slice comes to an end after a certain time known as the dispatcher minor time slice. If you have more work to do, you can stay in the dispatch list and get another time slice until you have finished (in which case you will be moved to the dormant list), or you will have to pay a visit to the scheduler again so that it can reassess your resource requirements before rescheduling you.

The scheduler may decide, after you have visited the dispatch list a few times, that you are not really an interactive user but that you need more processing capacity. You will then be upgraded to class 2 user and allowed to stay in the dispatch list for longer intervals to see whether you then manage to finish your work.

This has an additional benefit because it reduces the amount of policy decisions that the scheduler has to make to manage eligible users. A class 2 user might typically be a CMS user compiling programs, or a Linux Web server.

After you have visited the dispatch list as a class 2 user several times and still not finished your work, the scheduler will upgrade you to a class 3 user and you will be allowed to stay in the dispatch list even longer to see whether you manage to finish your work. Normally, a class 3 user will be a production guest operating system.

There are drawbacks to being a higher class user. For instance, if the system resources (such as paging or storage) become constrained, then the scheduler will hold higher class users in the eligible list and let lower class users run. However, there is one type of user, known as a class 0 user (it has OPTIONQUICKDSP in its directory entry or has had SET QUICKDSP issued on its behalf) who will never be held in the eligible list. Typically, this user type is only used for important servers and special user IDs.
