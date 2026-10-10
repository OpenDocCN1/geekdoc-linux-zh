login system for many users (via SSH, X, or VNC, for instance, as described in Chapter 21), chances are its load average will usually be above 1.0, as multiple people run programs simultaneously. Even a single-user system may end up running many CPU-intensive programs, and hence produce high load averages. Such a situation is to be expected on a multis user computer, server, or heavily used workstation, and doesn't necessarily indicate a problem.

In the end, excessive CPU demands are those that cause unacceptable performance. Of course, performance problems may be caused by factors other than CPU demands, such as insufficient RAM, as described in the upcoming section, “Monitoring Memory Use.” Thus, if your system isn't performing acceptably, then you can check CPU use and see if it's high. If the load average is above 1.0, and especially if it's well in excess of that value, such as 5.0, you may want to look more closely into CPU issues.

If top shows that your CPU time is being consumed by strange processes or by programs that you didn't realize were running, then you must correct the problem. There are also steps you can take to make the system seem more responsive even when the load average is high. Doing so is sometimes tricky, but a few tips can help you in this task.

# ### Correcting Problems

One CPU load problem that sometimes occurs involves *hung* processes. These are processes that have become unresponsive. Sometimes, hung processes do little harm, except for consuming memory. Other times, though, hung processes have hung because they've locked themselves into infinite loops. Such processes consume CPU time, typically imposing a 1.0 load average on an otherwise unloaded system. You can easily spot such processes by using `top`; they typically appear at or near the top of the process list. Of course, you can't simply assume that any program consuming a lot of CPU time is a hung process, so you should try to figure out who owns the process (specified in the `USERNAME` column) and what it does before you terminate the process.

You can use the `kill` program (described in the “kill and killall” section of Chapter 5) to terminate a hung process. For instance, suppose you've concluded that process 7297 is hung. You could issue the following command to kill it:

```
# kill 7297
```

You can then check to see if the process is still running. Most hung processes won't respond to a simple `kill` command, so you must take a firmer hand and pass the `KILL` signal (signal number 9), which tells FreeBSD to terminate the program without giving it a chance to close itself down:

```
# kill -KILL 7297
```

![](bbox=[0.88, 0.12, 0.99, 0.22])