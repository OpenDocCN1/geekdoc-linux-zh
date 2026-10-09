```
$last\ pid: 84111; load\ averages: 0.09, 0.21, 0.20 up
7+07:58:00 14:41:09
$28\ processes: 2\ running, 26\ sleeping
$CPU: 0.0%\ user, 0.0%\ nice, 0.9%\ system, 0.0%\ interrupt, 99.1%\ idle
$Mem: 80M\ Active, 642M\ Inact, 124M\ Laundry, 222M\ Wired, 17M\ Free
$Swap: 1024M\ Total, 83M\ Used, 941M\ Free, 8%\ Inuse

PID USERNAME THR PRI NICE SIZE RES STATE TIME WCPU COMMAND
479 bind 4 20 0 99444K 35956K kqread 6:55 0.00% named
586 root 1 20 0 154M 33768K select 4:54 0.00% perl
562 root 1 20 0 22036K 13948K select 1:27 0.00% ntpd
-- snip --
```

Very tightly packed, isn’t it? The top(1) tool crams as much data as possible into a standard 80 × 25 terminal window or X terminal. Let’s take this apart and learn how to read it. We’ll start with the upper part, which can look a little different depending on whether you’re using UFS or ZFS.

# UFS and top(1)

The per-host information at in the upper part of top(1) varies slightly between ZFS and UFS hosts, but we’ll start with UFS and then explain the differences.

# PID Values

Every process on a Unix machine has a unique process ID (PID). Whenever a new process starts, the kernel assigns it a PID one greater than the previous process. The last PID value is the last process ID assigned by the system. In the previous example, our last PID is 84,111. The next process created will be 84,112, then 84,113, and so on. Watch this number to see how fast the system changes. If the system is running through PIDs more quickly than usual, it might indicate a process forking beyond control or something crashing and restarting.

# Load Average

The load average is a somewhat vague number that offers a rough impression of the amount of CPU load on the system. The load average