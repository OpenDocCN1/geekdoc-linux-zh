
## Chapter 10: Tuning Oracle and RAC on Linux 251

Using 1 for instance number

*Specify the number of days of snapshots to choose from*

-----------------------------------------------

Entering the number of days (n) will result in the most recent
(n) days of snapshots being listed. Pressing <return> without
specifying a number lists all completed snapshots.

Listing all Completed Snapshots

| Instance | DB Name | Snap Id | Snap Started | Snap | Level Comment |
|---|---|---|---|---|---|
| orcl | ORCL | | 1 05 Jun 2004 22:41 | | 5 |
| | | | 2 06 Jun 2004 12:42 | | 5 |

Specify the Begin and End Snapshot Ids

-----------------------------------

Enter value for begin_snap: 1
Begin Snapshot Id specified: 1

Enter value for end_snap: 2
End Snapshot Id specified: 2

*Specify the Report Name*

-----------------------------------------------------

The default report file name is sp_1_2. To use this name,
press <return> to continue, otherwise enter an alternative. Enter
value for report_name:
userReport.txt
Using the report name JuneReport.txt

STATSPACK report for

This is followed by the Statspack report itself. In addition, the Statspack report is
written out to the file that was specified by your response to the questions that were
asked in the spreport.sql script.

Once you have a Statspack report, you are then ready to begin analysis into
what is going on in the Oracle instance, as well as some of the sessions.

## Interpreting Statspack Data

Statspack data is found in the report file that is created
by spreport.sql. This report has many Oracle statistics already calculated for you.
This information is very useful for both instance tuning and application tuning. A
few samples follow of what Statspack has to offer.
The Statspack report begins with information about the collection of data and
the Statspack report, as shown here:

STATSPACK report for

| DB Name | DB Id | Instance | Inst Num | Release | RAC Root |
|---|---|---|---|---|---|
| ORCL | 105394617 | orcl | 1 | 10.1.0.2.0 | NO |
| | | | | | ptc6.perftuning. |
| | | | | | com |

Snap Id | Snap Time | Sessions | Curs/Sess | Comment
---|---|---|---|---
Begin Snap: | 1 05-Jun-04 22:41:49 | 14 | 5.4 | 
End Snap: | 2 06-Jun-04 12:42:35 | 14 | 5.0 | 
Elapsed: | 840.77 (mins) | | | 

This is followed by information about the memory configuration and the load that the system has experienced during the measurement interval. This is shown here:

### Cache Sizes (end)

Buffer Cache: 24M Std Block Size: 8K
Shared Pool Size: 96M Log Buffer: 256K

### Load Profile

| | Per Second | Per Transaction |
|---|---|---|
| Redo size: | 647.77 | 7,103.81 |
| Logical reads: | 18.84 | 206.57 |
| Block changes: | 3.97 | 43.51 |
| Physical reads: | 0.58 | 6.37 |
| Physical writes: | 0.23 | 2.48 |
| User calls: | 0.06 | 0.68 |
| Parses: | 0.70 | 7.70 |
| Hard parses: | 0.01 | 0.07 |
| Sorts: | 0.48 | 5.25 |
| Logons: | 0.02 | 0.22 |
| Executes: | 1.65 | 18.08 |
| Transactions: | 0.09 | |

% Blocks changed per Read: 21.06 Recursive Call %: 99.26
Rollback per transaction %: 2.57 Rows per Sort: 10.07

Once the housekeeping has been taken care of and you have the background information, you can start looking at the actual tuning information. The first information that appears is cache information on the buffer cache and shared pool, as shown here:

### Instance Efficiency Percentages (Target 100%)

Buffer Nowait %: 100.00 Redo Nowait %: 99.99
Buffer Hit %: 96.62 In-memory Sort %: 100.00
Library Hit %: 99.35 Soft Parse %: 99.06
Execute to Parse %: 57.43 Latch Hit %: 100.00
Parse CPU to Parse Elapsed %: 93.74 % Non-Parse CPU: 69.69

| Shared Pool Statistics | Begin | End |
|---|---|---|
| Memory Usage %: | 70.36 | 83.46 |
| % SQL with executions>1: | 68.63 | 73.23 |
| % Memory for SQL w/exec>1: | 54.27 | 53.24 |

In addition to the cache statistics, numerous wait events and information on the SQL statements consuming the most resources and running for the longest time are listed and sorted by various resources. This can be very useful for finding the SQL that is consuming the most resources, and these statements are good candidates for tuning.

One thing that Statspack provides that is very useful is a list of the nondefault Oracle initialization parameters. This can be very helpful in determining if something obvious has been poorly tuned or not configured at all. This is usually my starting point for tuning a system: look for the obvious.

## Tuning for Wait Events

With the value of the Oracle statistics that are provided, you can often be quite effective by tuning Oracle SQL statements by using the wait events and session wait events. This information can often provide valuable information on what individual sessions are waiting on. Some common wait events are for buffers or latches. Because there are so many wait events, they will not be covered here in their entirety.

Several third-party tools available on the market, such as Indepth from Veritas, actually monitor the system by monitoring the wait events. If you know what events your system is waiting on, you can often tune it more effectively. Wait stats are a great way to tune the system because you are going right to the heart of the performance problem; the things that are taking the most time. Wait-based tuning can be quite effective but should be used in conjunction with other tuning methods, such as instance tuning and I/O tuning.

## Hardware Tuning

The third type of tuning is hardware tuning. Hardware tuning involves reconfiguring or adding new hardware to your system in order to improve performance. Hardware tuning is often necessary when you have exceeded the hardware resources of your system. This is most often the case with both the I/O subsystem and system RAM. When system resources have been consumed, and when efforts to tune the application and Oracle instance to reduce resource use have not improved performance enough, you really don't have much choice but to add more hardware.

Hardware tuning is similar in nature to sizing and capacity planning, which were covered earlier in this book.

Hardware usually should be the last resort; however, it is often the first resort. This is due to the fact that it is easier to add new hardware than to spend the time and effort to find out what the real problem is. This can sometimes work for a while, but eventually you get to the point where adding more hardware is either impossible or becomes prohibitively expensive. This is not to say that hardware tuning isn't necessary; it just shouldn't be the first step in tuning the system.

## Monitoring the Linux System

In addition to monitoring the Oracle system via Statspack, it is also important to monitor the Linux system. There are not very many parameters that you can tune in the Linux system, however, a poorly tuned system can experience severe performance problems because of that. Some of the parameters involve resources that must be allocated for Oracle, including shared memory and semaphores. As shown earlier in this book, these parameters can be set in the /etc/sysctl.conf parameter file. Let's look at a few of these parameters.

Shown here are the parameters set in /etc/sysctl.conf for shared memory and semaphores:

```
kernel.shmall = 2097152
kernel.shmmax = 2147483648
kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
```

These parameters configure how large the shared memory segment can be. With this setting, you could have an SGA that is up to 2GB in size (assuming no other programs are using shared memory). In order to view the shared memory and semaphores that are currently in use, use the Linux ipcs command, as shown here:

```
[root@ptc6 root]# ipcs

-------- Shared Memory Segments ----------
key        shmid    owner    perms      bytes      nattch     status
0x00005643 0        root     666        1024       1
0x00005654 32769    root     666        1024       1
0x00000000 262146   gdm      777        196608     2          dest
0x00000000 327683   gdm      777        196608     2          dest
0x54250c38 360452   oracle   640        188747776  15

-------- Semaphore Arrays -----------
key        semid    owner    perms      nsems      status
0x00005653 0        root     666        1
0x460de1d4 196609   oracle   640        127
0x460de1a5 327978   oracle   640        127
0x460de1a6 262147   oracle   640        127

--------- Message Queues --------
key        msqid    owner    perms      used-bytes   messages
```

Additional tuning parameters that are needed to install Oracle include the following:

```
fs.file-max = 65536
net.ipv4.ip_local_port_range = 1024 65000
```
