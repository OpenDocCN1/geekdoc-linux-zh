problems can create network problems and vice versa. In this section I will cover problems that occur specifically on a host and leave issues that impact the network to the next section.

# Host Is Sluggish or Unresponsive

Probably one of the most common problems you will find on a host is that it is sluggish or completely unresponsive. Often this can be caused by network issues, but here I will discuss some local troubleshooting tools you can use to tell the difference between a loaded network and a loaded machine.

When a machine is sluggish, it is often because you have consumed all of a particular resource on the system. The main resources are CPU, RAM, disk I/O, and network (which I will leave to the next section). Overuse of any of these resources can cause a system to bog down to the point that often the only recourse is your last resort—a reboot. If you can log in to the system, however, there are a number of tools you can use to identify the cause.

# System Load

System load average is probably the fundamental metric you start from when troubleshooting a sluggish system. One of the first commands I run when I’m troubleshooting a slow system is uptime:

```
$ uptime
13:35:03 up 103 days, 8 min, 5 users, load average: 2.03, 20.17, 15.09
```

The three numbers after the load average, 2.03, 20.17, and 15.09, represent the 1-, 5-, and 15-minute load averages on the machine, respectively. A system load average is equal to the average number of processes in a runnable or uninterruptible state. Runnable processes are either currently using the CPU or waiting to do so, and uninterruptible processes are waiting for I/O. A single-CPU system with a load average of 1 means the single CPU is under constant load. If that single-CPU system has a load average of 4, there is 4 times the load on the system that it can handle, so three out of four processes are waiting for resources. The load average reported on a system is not tweaked based on the number of CPUs you have, so if you have a two-CPU system with a load average of 1, one of your two CPUs is loaded at all times—i.e., you are 50% loaded. So a load of 1 on a single-