shell's version rather than the operating system's. This duplication can be confusing because shell-nice and command-nice use different syntax: the shell wants its priority increment expressed as +incr or -incr, but the stand-alone command wants an -n flag followed by the priority increment.*

Table 5.3 summarizes all these variations. A prio is an absolute nice value, while an incr is relative to the niceness of the shell from which nice or renice is run. Wherever an -incr or a -prio is called for, you can use a double dash to enter negative values (e.g., --10). Only the shell nice understands plus signs (in fact, it requires them); leave them out in all other circumstances.

# Table 5.3 How to express priorities for various versions of nice and renice

| System | Range | OS nice | csh nice | renice |
|---|---|---|---|---|
| Linux | -20 to 19 | -incr or -n incr | +incr or -incr | prio |
| Solaris | 0 to 39 | -incr or -n incr | +incr or -incr | incr or -n incr |
| HP-UX | 0 to 39 | -prio or -n prio | +incr or -incr | -n prio* |
| AIX | -20 to 19 | -incr or -n incr | +incr or -incr | -n incr |

a. Uses absolute priority, but adds 20 to the value you specify.

The most commonly niced process in the modern world is ntpd, the clock synchronization daemon. Since promptness is critical to its mission, it usually runs at a nice value about 12 below the default (that is, at a higher priority than normal).

If a problem drives the system's load average to 65, you may need to use nice to start a high-priority shell before you can run commands to investigate the problem. Otherwise, you may have difficulty running even simple commands.

# 5.7 PS: MONITOR PROCESSES

ps is the system administrator's main tool for monitoring processes. While versions of ps differ in their arguments and display, they all deliver essentially the same information. Part of the enormous variation among versions of ps can be traced back to differences in the development history of UNIX. However, ps is also a command that vendors tend to customize for other reasons. It's closely tied to the kernel's handling of processes, so it tends to reflect all of a vendors' underlying kernel changes.

ps can show the PID, UID, priority, and control terminal of processes. It also gives information about how much memory a process is using, how much CPU time it has consumed, and its current status (running, stopped, sleeping, etc.). Zombies show up in a ps listing as <exiting> or <defunct>.