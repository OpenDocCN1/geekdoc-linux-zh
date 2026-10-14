
2. Use `clu_quorum` to make sure the cluster will not lose quorum when you halt the hung member. (Reference Chapter 17.)

3. Crash the hung member by manually halting the member and running “crash” at the console prompt.

```text
>>> crash
```

4. Boot the previously hung member. During boot, `savecore(8)` runs and captures the dump in `/var/adm/crash`. If the system won't boot, try booting to single-user and collect the crash files manually:

```sh
# /sbin/checkrc
# /sbin/init.d/savecore
# /sbin/init.d/crashd
```

This should create the crash files in the default location (`/var/adm/crash`).

You should send the crash files to HP Support for analysis.

## A.1.3 System is Running Slowly

If your cluster member(s) is running slowly, you should run the usual tools to try and identify the subsystem and, if possible, the specific offending element much like on a standalone system.

- `vmstat(1)`  
  You should have healthy idle time (usually non-zero), zero or near zero pageouts, and healthy free list size (greater than the `vm_page_free_target` — `sysconfig -q vm vm_page_free_target`).

- `netstat(1)`  
  Look for heavy activity and especially collisions (if Ethernet). Collisions greater than 10% of traffic are usually a bad sign, but this is not a hard and fast rule.

- `collect(8)`  
  Use collect for just about all of your performance gathering needs, but the I/O stats are particularly helpful. Watch for any disks getting overwhelmed. What is considered overwhelmed? That’s outside the scope of this book, but it’s a factor of the HBA, storage subsystem, and individual disk(s) themselves. Historical data is also a good guide to see if disks (or anything else for that matter) are being exhausted more than usual.

```text
# collect -d d
Initializing (10.0 seconds) ... done.

#### RECORD 1 (1032229234:0) (Mon Sep 16 22:20:34 2002) ####

# DISK Statistics
#DSK   NAME   %/T/  RAS R/W/S  W/S WKB/S  AVS  AWA  AWO  WIO  %BSY
 0    cdrom0  0/5/0    0     0    0    0.00 0.00 0.00 0.00 0.00
 1    dskc0   1/0/0    0     0    0   13.33 0.00 0.00 0.00 0.10
 2    dsk9    2/0/1    0     0    0    0.00 0.00 0.00 0.00 0.00
 3    dsk10   2/0/2    0     0    0    0.00 0.00 0.00 0.00 0.00
 4    dsk11   2/0/3    0     0    0    0.00 0.00 0.00 0.00 0.00
 5    dsk12   2/0/4    0     0    0    0.00 0.00 0.00 0.00 0.00
 6    dsk13   2/0/5    0     0    0    0.00 0.00 0.00 0.00 0.00
 7    dsk14   2/0/6    0     0    0    0.00 0.00 0.00 0.00 0.00
 8    dsk1    2/1/0    3   139    0   21.37 0.00 0.07 0.00 5.49
 9    dsk2    2/1/1   15  1943    0   22.83 0.00 0.36 0.00 21.47
10    dsk3    2/1/2    0     0    0    0.00 0.00 0.00 0.00 0.00
11    dsk4    2/1/3    0     0    0    0.00 0.00 0.00 0.00 0.00
12    dsk5    2/1/4    0     0    0    0.00 0.00 0.00 0.00 0.00
13    dsk6    2/1/5    2   170    0   30.42 0.00 0.08 0.00 6.69
14    dsk7    2/1/6    0     0    0   17.50 0.00 0.01 0.00 0.70
15    dsk8    2/1/7    0     0    0    0.00 0.00 0.00 0.00 0.00
16    dsk18   2/2/0    0     0    0    0.00 0.00 0.00 0.00 0.00
17    dsk19   2/2/1    0     0    0    0.00 0.00 0.00 0.00 0.00
18    dsk20   2/2/2    0     0    0    0.00 0.00 0.00 0.00 0.00
```

In this case, dsk2 is getting some activity, but it isn’t bad: 21.47% BSY (busy).

- `ps(1)`  
  This command lists the current processes. If the performance problem is a single process, you’ll get a good idea of that from this output. Using the “pcpu” keyword, you can see the current top CPU users.

```text
# ps -eo pcpu,etime,user,pid,comm | sort -r | head
%CPU       TIME USER       PID COMMAND
 5.2    16:40.18 monboot  1132662 monboot-2.3.7
 4.4    11:54.07 gry      1168434 x18t133tsp34k0
 1.3     0:00.04 root     1138862 sshd
 0.6    02:46.58 root     1048576 kernel_idle
 0.2    13:31.87 aey      1049022 more README
 0.0     9:17.01 root     1048088 evmd
 0.0     5:21.51 cjy      1052689 telnet justice
 0.0     3:04.06 root     1048692 update
 0.0     2:32.01 bly      1052606 ksh
```

We might have used `ps aux | head` here but the formatted output was difficult to read. You can use either command or roll your own.
