
## Listing 13-8: Profiling Using ltrace

```
$ ltrace -c ./example
$HOME = /home/chris
%
time        seconds  uses/call calls function
24.16 0.000231        231   1 printf
16.53 0.000158        158   1 fclose
16.00 0.000153        153   1 fopen
13.70 0.000131        131   1 malloc
10.67 0.000102        102   1 remove
9.31 0.000089         89   1 fprintf
3.35 0.000032         32   1 getenv
3.14 0.000030         30   1 free
3.14 0.000030         30   1 strncpy
100.00 0.000956 9 total
```

The ltrace tool is available only for programs that have been compiled to use dynamically linked shared library objects. This is the usual default, so unless you explicitly specify -static when compiling, you can use ltrace on the resulting binary. Again similar to strace, you must use an ltrace binary that has been compiled for your target architecture. These utilities are run on the target, not the host development system.

### 13.4.4 ps

With the possible exception of strace and ltrace, no tools are more often neglected by the embedded systems developer than top and ps. Given the myriad options available for each utility, we could easily devote an entire chapter to these useful system-profiling tools. They are almost universally available in embedded Linux distributions.

Both of these utilities make use of the /proc file system, as described in Chapter 9, "File Systems." Much of the information they convey can be learned from the /proc file system if you know what to look for and how to parse the resulting information. These tools present that information in a convenient human-readable form.

The ps utility lists all the running processes on a machine. However, it is very flexible and can be tailored to provide much useful data on the state of a running machine and the processes running on it. For example, ps can display the scheduling policy of each process. This is particularly useful for systems that employ real-time processes.

Without any options, ps displays all processes with the same user ID as the user who invoked the command, and only those processes associated with the terminal on which the command was issued. This is useful when many jobs have been spawned by that user and terminal.

Passing options to ps can be confusing because ps supports a wide variety of standards (as in POSIX versus UNIX) and three distinct options styles: BSD, UNIX, and GNU. In general, BSD options are single or multiple letters, with no dash. UNIX options are the familiar dash-letter combinations, and GNU uses long argument formats preceded by double dashes. Refer to the man page for details of your ps implementation.

Everyone who uses ps likely has a favorite invocation. One particularly useful general-purpose invocation is ps aux. This displays every process on the system. Listing 13-9 is an example from a running embedded target board.

## Listing 13-9: Process Listing

```
$ ps aux
USER      PID  %CPU %MEM   VSZ  RSS TTY  STAT START    TIME COMMAND
root        1   0.0  0.8  1416  508 ?    S    00:00  0:00 init [3]
root        2   0.0  0.0    0    0 ?    S?   00:00  0:00 [ksoftirqd/0]
root        3   0.0  0.0    0    0 ?    S<   00:00  0:00 [khelper/0]
root        4   0.0  0.0    0    0 ?    S    00:00  0:00 [events/0]
root        5   0.0  0.0    0    0 ?    S<   00:00  0:00 [khelper/]
root       10   0.0  0.0    0    0 ?    S<   00:00  0:00 [kthread]
root       21   0.0  0.0    0    0 ?    S<   00:00  0:00 [khblockd/0]
root       62   0.0  0.0    0    0 ?    S    00:00  0:00 [pdflush]
root       63   0.0  0.0    0    0 ?    S    00:00  0:00 [pdflush]
root       65   0.0  0.0    0    0 ?    S<   00:00  0:00 [aio/0]
root       36   0.0  0.0    0    0 ?    S    0:00    [kswapd]
root       64   0.0  0.0    0    0 ?    S    0:00    [kswapd0]
root      617   0.0  0.0    0    0 ?    S    0:00    [khubd]
root      638   0.0  0.0    0    0 ?    S    0:00    [kthread]
root      834   0.0  0.7 1568  444 ?    Ss   0:00    /sbin/portmap
bin       861   0.0  0.0    0    0 ?    S    0:00    [lockd]
root      868   0.0  0.9 1488  596 ?    Ss   0:00    /sbin/syslogd -r
root      876   0.0  0.7  412  456 ?    Ss   0:00    /sbin/klogd -x
root      884   0.0  1.1 1660  700 ?    Ss   0:00    /usr/sbin/rpc.statd
root      896   0.0  0.9 1688  584 ?    Ss   0:00    /usr/sbin/inetd
root      909   0.0 2.2 2412 1372 ?    Ss   0:00    /usr/sbin/xinetd
telnetd   953   0.1 1.1 1736  732 ?    S<   05:58  0:00 in.telnetd
root      954  0.2 2.1 2384 1348 pts/0 S   05:58  0:00 -bash
root      960   0.0 1.2 2312  772 pts/0 R+ 05:59  0:00 ps aux
```

This is but one of the many ways to view output data using ps. The columns are explained in the following text.

- The USER and process ID (PID) fields should be self-explanatory.
- The %CPU field expresses the percent of CPU utilization since the beginning of the process's lifetime; thus, CPU usage will virtually never add up to 100 percent.
- The %MEM field indicates the ratio of the process's resident memory footprint to the total available physical memory.
- The VSZ field is the virtual memory size of the process in kilobytes.
- RSS is resident set size and indicates the nonswapped physical memory that a process has used, also in kilobytes.
- TTY is the controlling terminal of the process.

Most of the processes in this example are not associated with a controlling terminal. The ps command that generated Listing 13-9 was issued from a Telnet session, which is indicated by the pts/0 terminal device.

The STAT field describes the state of the process at the time this snapshot was produced. Here, S means that the process is sleeping, waiting on an event of some type, often I/O. R means that the process is in a runnable state (that is, the scheduler is free to give it control of the CPU if nothing of a higher priority is waiting). The left bracket next to the state letter is an indication that this process has a higher priority.

The final column is the command name. Those listed in brackets are kernel threads. Many more symbols and options are available; refer to the man page for ps for complete details.

### 13.4.5 top

Whereas ps is a one-time snapshot of the current system, top takes periodic snapshots of the state of the system and its processes. Similar to ps, top has numerous command line and configuration options. It is interactive and can be reconfigured while operating to customize the display to your particular needs.

Entered without options, top displays all running processes in a fashion very similar to the ps aux command presented in Listing 13-9, updated every 3 seconds. Of course, this and many other aspects of top are user configurable. The first few lines of the top screen display system information, also updated every 3 seconds. This includes the system uptime, the number of users, information on the number of processes and their state, and much more.

Listing 13-10 shows top in its default configuration, resulting from executing top from the command line without parameters.

## Listing 13-10

```
top

top - 06:23:14 up 6:23,  2 users,  load average: 0.00, 0.00, 0.00
Tasks: 24 total,   1 running,  23 sleeping,   0 stopped,   0 zombie
Cpu(s): 0.0% us,  0.3% sy,  0.0% ni, 99.7% id,  0.0% wa,  0.0% hi,  0.0% si
Mem:  62060k total,  12792k used,   44768k free,   1164k cached
Swap:       0k total,        0k used,        0k free,        0k cached

  PID USER   PR NI  VIRT  RES  SHR S %CPU %MEM    TIME+ COMMAND
  978 root   16  0  1924  952 780 R   0.3   1.5   0:01.22 top
    1 root   16  0  1416  508 452 S   0.0   0.8   0:00.47 init
    2 root    5 -10   0    0    0 S   0.0   0.0   0:00.00 keventirqd/0
    3 root    5 -10   0    0    0 S   0.0   0.0   0:00.00 desched/0
    4 root   -2  -5   0    0    0 S   0.0   0.0   0:00.00 events/0
    5 root   -2  -5   0    0    0 S   0.0   0.0   0:00.09 khelper
   10 root   18  -5   0    0    0 S   0.0   0.0   0:00.00 kthread
   21 root   20  -5   0    0    0 S   0.0   0.0   0:00.00 blkdeiod/0
   62 root   20   0   0    0    0 S   0.0   0.0   0:00.00 kdiush
   63 root   15   0   0    0    0 S   0.0   0.0   0:00.00 pidflush
   65 root   19  -5   0    0    0 S   0.0   0.0   0:00.00 kid/0
   36 root   25   0   0    0    0 S   0.0   0.0   0:00.00 kapid
   64 root   25   0   0    0    0 S   0.0   0.0   0:00.00 kawpd/0
   61 root   25   0   0    0    0 S   0.0   0.0   0:00.00 mdblockd
   638 root   15   0   0    0    0 S   0.0   0.0   0:00.34 rpciod
   834 bin    15   0  1568 444 364 S   0.0   0.7   0:00.00 portmap
   861 root   20   0  3144   0    0 S   0.0   0.0   0:00.00 koiod
   868 root   16   0 1488 596 504 S   0.0   1.0   0:00.11 sysloadg
   876 root   19   0 1416 456 396 S   0.0   0.7   0:00.02 kircd
   884 root   18   0  1660  700 612 S   0.0   1.1   0:0*.02 rpc.statd
   896 root   16   0  1668 584 504 S   0.0   0.9   0:00.00 inetd
   988 root   15   0 2412 1372 1092 S   0.0   2.2   0:00.34 bash
  953 telnetd 16   0  1736  736 616 S   0.0   1.2   0:00.27 telnetd
  954 root   15   0 2384 1348 1096 S   0.0   2.2   0:00.16 bash
```
