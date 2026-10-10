![](bbox=[0.15, 0.1, 0.85, 0.54])

# Figure 28-1. The top utility enables you to locate CPU-hogging programs.

> The CPU times reported by top aren't directly comparable to uptime's load averages. The top percentages never exceed 100%; they're measures of actual CPU allocations, whereas uptime reports demand for CPU time, and so can exceed 1.0.

Several other columns in top's output can be important in certain circumstances. The most important of these is the PID column, which shows the process ID of the program. You may need to use this information to kill or reprioritize a program that's consuming an inordinate amount of CPU time. The program's owner, as reported by the USERNAME column, may also be important in helping to identify users who regularly run CPU-intensive programs.

# Knowing When CPU Use Is Excessive

Unfortunately, there's no simple rule to tell you when CPU use on any given computer is excessive. Although programs don't get the best possible performance on your hardware when the load average climbs above 1.0, using 1.0 as a cutoff for an acceptable CPU load may not be a reasonable criterion. If your FreeBSD computer functions as a remote