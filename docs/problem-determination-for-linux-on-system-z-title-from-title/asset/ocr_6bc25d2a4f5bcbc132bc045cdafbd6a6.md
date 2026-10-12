As we can see in Example 11-2 on page 318, the system is hardly utilizing the available processors, but, at the same time, it is able to manage the workload with the available memory efficiently. In the case of the DB2 server, however, both the processor and memory are not fully utilized, as shown in Example 11-3.

# Example 11-3 DB2 server utilization

```
top - 18:15:30 up 3 min, 1 user, load average: 0.02, 0.03, 0.00
Tasks: 83 total, 2 running, 81 sleeping, 0 stopped, 0 zombie
Cpu(s): 0.7%us, 0.3%sy, 0.0%ni, 99.0%id, 0.0%wa, 0.0%hi, 0.0%si, 0.0%st
Mem: 2048816k total, 344008k used, 1704808k free, 7876k buffers
Swap: 719896k total, 0k used, 719896k free, 251156k cached

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
2390 db2inst1 15 0 172m 11m 8104 S 0 0.6 0:00.13 db2sysc
2413 db2inst1 15 0 172m 11m 8004 S 0 0.6 0:00.06 db2sysc
2462 db2inst1 15 0 172m 11m 7988 S 0 0.6 0:00.03 db2sysc
2469 root 16 0 2640 1300 980 R 0 0.1 0:00.05 top
1 root 16 0 848 316 264 S 0 0.0 0:00.50 init
```

Then we looked at the application server. It was consuming all of the memory that we had allocated to it (see Example 11-4). So we narrowed it down to the application server for further investigation. We also wanted to know the problem from the hardware resources perspective only.

# Example 11-4 WAS server utilization

```
top - 18:15:30 up 3 min, 1 user, load average: 0.02, 0.03, 0.00
Tasks: 53 total, 1 running, 52 sleeping, 0 stopped, 0 zombie
Cpu(s): 0.2%us, 1.3%sy, 0.0%ni, 98.1%wa, 0.0%hi, 0.3%si, 0.0%st
Mem: 2048816k total, 1951484k used, 97332k free, 232k buffers
Swap: 719896k total, 0k used, 719892k free, 44500k cached

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
1521 root 17 0 2551m 1.5g 54m S 21.7 78.5 2:24.74 java
68 root 15 0 0 0 1.7 0.0 0:00.40 kswapd0
1 root 17 0 848 68 44 D 0.3 0.0 0:00.51 init
4 root 10 -5 0 0 0 S 0.0 0.0 0:00.06 events/0
2 root RT 0 0 0 0 S 0.0 0.0 0:00.00 migration/0
3 root 34 19 0 0 0 0 S 0.0 0.0 0:00.00 ksoftirqd/0
5 root 17 -5 0 0 0 S 0.0 0.0 0:00.00 khelper
6 root 10 -5 0 0 0 S 0.0 0.0 0:00.00 kthread
```