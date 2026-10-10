
![](img/f34d37e3abe9f4517128e54f80ab2616_719_0.png)

## Figure 28-1. The top utility enables you to locate CPU-hogging programs.

> The CPU times reported by top aren't directly comparable to uptime's load averages. The top percentages never exceed 100%; they're measures of actual CPU allocations, whereas uptime reports demand for CPU time, and so can exceed 1.0.

Several other columns in top's output can be important in certain circumstances. The most important of these is the PID column, which shows the process ID of the program. You may need to use this information to kill or reprioritize a program that's consuming an inordinate amount of CPU time. The program's owner, as reported by the USERNAME column, may also be important in helping to identify users who regularly run CPU-intensive programs.

## Knowing When CPU Use Is Excessive

Unfortunately, there's no simple rule to tell you when CPU use on any given computer is excessive. Although programs don't get the best possible performance on your hardware when the load average climbs above 1.0, using 1.0 as a cutoff for an acceptable CPU load may not be a reasonable criterion. If your FreeBSD computer functions as a remote login system for many users (via SSH, X, or VNC, for instance, as described in Chapter 21), chances are its load average will usually be above 1.0, as multiple people run programs simultaneously. Even a single-user system may end up running many CPU-intensive programs, and hence produce high load averages. Such a situation is to be expected on a multiuser computer, server, or heavily used workstation, and doesn't necessarily indicate a problem.

In the end, excessive CPU demands are those that cause unacceptable performance. Of course, performance problems may be caused by factors other than CPU demands, such as insufficient RAM, as described in the upcoming section, “Monitoring Memory Use.” Thus, if your system isn't performing acceptably, then you can check CPU use and see if it's high. If the load average is above 1.0, and especially if it's well in excess of that value, such as 5.0, you may want to look more closely into CPU issues.

If top shows that your CPU time is being consumed by strange processes or by programs that you didn't realize were running, then you must correct the problem. There are also steps you can take to make the system seem more responsive even when the load average is high. Doing so is sometimes tricky, but a few tips can help you in this task.

### Correcting Problems

One CPU load problem that sometimes involves *hung* processes. These are processes that have become unresponsive. Sometimes, hung processes do little harm, except for consuming memory. Other times, though, hung processes have hung because they've locked themselves into infinite loops. Such processes consume CPU time, typically imposing a 1.0 load average on an otherwise unloaded system. You can easily spot such processes by using `top`; they typically appear at or near the top of the process list. Of course, you can't simply assume that any program consuming a lot of CPU time is a hung process, so you should try to figure out who owns the process (specified in the `USERNAME` column) and what it does before you terminate the process.

You can use the `kill` program (described in the “kill and killall” section of Chapter 5) to terminate a hung process. For instance, suppose you've concluded that process 7297 is hung. You could issue the following command to kill it:

```
# kill 7297
```

You can then check to see if the process is still running. Most hung processes won't respond to a simple `kill` command, so you must take a firmer hand and pass the `KILL` signal (signal number 9), which tells FreeBSD to terminate the program without giving it a chance to close itself down:

```
# kill -KILL 7297
```

![](img/f34d37e3abe9f4517128e54f80ab2616_720_0.png)

You can also use killall to kill a process by name rather than by number. Doing so can save you the bother of looking up a PID if you know a process is hung. On the down side, killall kills all processes of a given name, so if one process has hung but others of the same name are running normally, you'll terminate the processes that are not causing problems, as well as the troubled one.

A less extreme problem involves a process that’s running legitimately but that’s consuming a lot of CPU time. Such a process can degrade performance, making the computer seem sluggish to users. You might want to run a CPU-intensive program that you know will take a long time to finish its work, but you might also want to run less CPU-intensive programs. For instance, distributed computing projects such as SETI@Home (http://setiathome.ssl.berkeley.edu) chew up lots of CPU cycles, but you probably don’t want them to degrade your use of a computer for word processing, web browsing, or the like. You can use the nice command to launch another program with reduced priority, or use renice to change a process’s priority. The “nice and renice” section of Chapter 5 describes these commands in more detail. As a problem-correcting tool, renice is more useful because it enables you to reduce the priority of a CPU-hogging process that’s already running. For instance, suppose a small multiuser system normally has a load average of between 1 and 2, but it jumps to 3 one day because of one user’s CPU-intensive program. Once you’ve identified that program as PID 7297 with top, you can issue the following command to reduce its priority:

```
$ renice 10 7297
```

The first number in this command, 10, is the process’s new priority. Most FreeBSD processes have a priority of 0. Higher priority numbers indicate decreased priority, with the lowest-priority process having a value of 20. Thus, a value of 10, as in this example, is a good starting point for reducing a process’s priority.

The disadvantage of reducing a process’s priority is that the process is likely to finish its work later than it otherwise would because it gets less CPU time than competing processes. This situation is certainly likely to be true in the example of a CPU-intensive process running on a system that normally has a load average of 2.0. Reducing the priority of a CPU-intensive process on a computer that’s otherwise lightly loaded (that is, with a load average of well under 1.0) is unlikely to have a great impact on the process’s completion time because it will still get CPU cycles whenever other processes don’t need them, which is most of the time.

### Preventing Problems

You can take several steps to help prevent CPU load problems:

- **Buy appropriate hardware** If you know a system will support many users or CPU-intensive programs, be sure to equip it with a fast enough CPU. Unfortunately, it's hard to define precisely what “fast enough” is. As a hedge against CPU problems, you may want to buy a computer with a motherboard that supports a substantially faster CPU than the CPU that you buy; that way, if your CPU turns out to be inadequate, you can upgrade it without upgrading the motherboard.
- **Run efficient programs** Some programs run more efficiently than others. Compiling a program with optimizations for your particular CPU may gain a modest performance improvement, but sometimes more dramatic improvements can be gained by replacing an inefficient program with another program that uses more efficient algorithms. You’ll have to research efficiency issues on a program-by-program basis.
- **Run fewer programs** Running many programs can degrade performance. For instance, Figure 28-1 reveals that x11amp (an MP3 player described in Chapter 27) consumes close to half of the CPU time on the target computer (which has a weak CPU by today’s standards—a 233MHz AMD K6). Shutting down this program will free a lot of CPU time for potentially more important programs.
- **Use nice** You can launch CPU-intensive programs with nice to reduce their impact on more interactive programs. For instance, *nice* cpushog launches the cpushog program with a priority of 10, reducing its impact on other programs.
- **Regularly check CPU load** Particularly on multiuser systems, you should check the CPU load on a regular basis. If you notice a sudden increase in average load, you may be seeing the effect of a hung process. Although there’s little you can do to actually prevent processes from hanging, killing them quickly can prevent users from becoming annoyed by reduced performance.

## Monitoring Memory Use

FreeBSD is designed to hide details of memory use from the average user, and even from the average program. Every program is given its own memory space that’s separate from the memory space of all other programs. The kernel manages all programs’ allocated memory. When necessary, the kernel uses *swap space* (disk space that extends physical memory, as described in Chapter 7 and elsewhere) to run programs that won’t fit in physical memory. Swap space, though, is much slower than physical memory, and if memory demands are too great, you can run out of swap space. These facts mean that if your system’s memory demands are high enough, the system will slow down; and if they’re higher still, programs may refuse to run or even crash. For these reasons, it’s important to monitor the memory use of a FreeBSD system.

![](img/f34d37e3abe9f4517128e54f80ab2616_722_0.png)
