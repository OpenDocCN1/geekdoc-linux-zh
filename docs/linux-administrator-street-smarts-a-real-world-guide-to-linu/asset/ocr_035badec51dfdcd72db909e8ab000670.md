# Caveats

This task presents few risks, although when performing real-life process management as **root**, the usual `root` caveats apply. It's possible that you'll terminate the wrong process if you enter a typo, and this risk can have more serious consequences when you work as **root**—you could accidentally terminate a critical server, for instance.

# Procedure

To perform this task, you'll use three process-monitoring tools. First, you'll check the overall system load—that is, how much of the system's available CPU time all the running programs are demanding. Second, you'll obtain static process listings. Third, you'll use a dynamic tool that's particularly helpful for spotting processes that are out of control. Once you've identified an out-of-control process, you can terminate it.

# Checking System Load

The system load is most often measured as a *load average*, which is a number from 0 upward. A load average of 0.0 means that no processes are demanding CPU time. A load average of 1.0 means that programs are demanding exactly as much CPU time as the CPU has to offer. A load average greater than 1.0 means that programs are demanding more CPU time than is available, requiring the kernel to ration CPU time. Typically, load averages are measured over some period of time, such as the last minute or the last 5 minutes.

Lightly loaded systems often have load averages between 0.0 and 1.0. Such systems perform as well as they can, given the efficiency of the code they run and the speed of the CPU. (Such systems could be sluggish because of poor disk performance or other reasons, though; load averages only tell you about demands on CPU time.) When the load average climbs above 1.0, efficiency drops—programs become sluggish because they must compete with other programs for CPU time. Thus, ideally your system's load average shouldn't rise above 1.0.

In practice, though, load averages do often exceed 1.0, particularly for short periods of time. If you run a CPU-intensive program in the background and also do something else, the load average will rise above 1.0, although perhaps not by much—it might reach 1.3 or so. Systems that are intended as multi-user computers often have load averages well over 1.0, and this isn't necessarily a problem if the CPU is fast enough. For instance, if System A has a CPU load of 2.0 and a CPU that's three times as fast as System B, System A may be faster than System B. The easiest way to check your system load is to use the `uptime` command, which displays the amount of time the system has been running, the number of users who are logged in, and the load averages over the past 1, 5, and 15 minutes:

```
$ uptime
13:24:49 up 31 days, 17:24, 6 users, load average: 2.34, 2.28, 1.79
```

> **NOTE** The number of users reported by `uptime` is the number of simultaneous logins of various types. All of these logins could be by the same user.