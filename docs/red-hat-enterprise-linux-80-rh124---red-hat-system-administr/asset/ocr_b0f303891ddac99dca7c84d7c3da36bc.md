If the main contribution to load average is from processes waiting for the CPU, you can calculate the approximate per CPU load value to determine whether the system is experiencing significant waiting.

The lscpu command can help you determine how many CPUs a system has.

In the following example, the system is a dual-core single socket system with two hypertheads per core. Roughly speaking, Linux will treat this as a four CPU system for scheduling purposes.

```
[user@host ~]$ lscpu
Architecture: x86_64
CPU op-mode(s): 32-bit, 64-bit
Byte Order: Little Endian
CPU(s): 4
On-line CPU(s) list: 0-3
Thread(s) per core: 2
Core(s) per socket: 2
Socket(s): 1
NUMA node(s): 1... omitted.
```

For an moment, the only contribution to load average is from processes that need CPU time. Then you can display the load average values by the number of CPUs in the system. A value below i indicates satisfactory resource utilization and minimal wait times. A value above i indicates resource saturation and some amount of processing delay.

```
# From lscpu, the system has four logical CPUs, so divide by 4:
# load average: 2.92, 4.48, 5.20
# number of logical CPUs: 4

# per-CPU load average: 0.73 1.12 1.30
```

# This system's load average appears to be decreasing.
# With a load average of 2.92 on four CPUs, all CPUs were in use ~73% of the time.
# During the last 5 minutes, the system was overloaded by -12%.
# During the last 15 minutes, the system was overloaded by -30%.

An idle CPU queue has a load number of 0. Each process waiting for a CPU adds a count of 1 to the load number. If one process is running on a CPU, the load number is one, the resource (the CPU) is in use, but there are no requests waiting. If process is running for a full minute, its contribution to the one-minute load average will be 1.

However, processes uninterruptibly serving for critical I/O to a busy disk or network resource are also included in the count and increase the load average. While not an indication of CPU utilization, these processes are added to the queue because they are waiting for resources and cannot run on a CPU until they get them. This is system load due to resource limitations that is causing processes not to run.

Until resource saturation, a load average remains below 1, since tasks are found wound in waiting queue. Load average only increases when resource saturation requests to remain queued and are counted by the load calculation routine. When resource utilization approaches 100%, each additional request starts experiencing service wait.

A number of additional tools report load average, including w and top.