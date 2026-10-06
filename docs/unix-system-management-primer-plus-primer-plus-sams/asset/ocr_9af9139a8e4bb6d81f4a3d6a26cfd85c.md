# Chapter 11 • PERFORMANCE TUNING AND CAPACITY PLANNING 25

No hard and fast rule dictate the maximum rate of context switching; the variety of processes, hardware, and operating systems in use today makes this rate impossible to calculate. To monitor your system's context-switching rate, first determine what rate is normal for your system, then watch for variations from that rate. If a system usually has 500 to 1,000 contexts per second, you know there is a problem when that number shoots up to 3,000. In that case, you could trace the running process to see exactly what the process is trying to do (you learn more about tracing in "Tracing Processes," in this chapter).

After you have determined that user processes are responsible for your high load, it's not hard to figure out what processes are causing that load. All Unix systems have commands to help you analyze processes—two of the most useful ones are ps and top.

# Using ps to Monitor CPU Usage by Process

The ps command is available on all Unix platforms, but few people use it to measure CPU usage. Because ps is available everywhere, however, you can use it to analyze CPU usage on any Unix Version. The output of ps can be verbose, but only the column of interest for this measurement is TIME, which reports the amount of time a process has spent running on a CPU. While individual TIME statistics tell you how busy a process has been up to that point, running repeated ps commands can tell you if a process's CPU time is increasing.

For example, on a heavily loaded Oracle database server, ps gave the following output for one of the Oracle processes over several seconds:

| PID | TIME CMD |
|---|---||
| 121 ? | 100:45 oracle |
| 121 ? | 100:46 oracle |
| 121 ? | 100:46 oracle |
| 121 ? | 100:46 oracle |
| 121 ? | 100:47 oracle |
| 121 ? | 100:47 oracle |
| 121 ? | 100:47 oracle |
| 121 ? | 100:47 oracle |
| 121 ? | 100:47 oracle |
| 121 ? | 100:48 oracle |

The Oracle process, having already used over 100 minutes of CPU time, increases slowly and consumes an additional second of CPU time over a 4-second interval. This equates to 25% of a CPU's time, so this process should definitely be investigated further.

![](bbox=[0.105, 0.755, 0.715, 0.785])

Most processes do not use CPU time at all, and won't register a second of CPU time during their lifetime.

# Using top to Monitor Process CPU Usage

Using ps to look for CPU-intensive processes can be a cumbersome task when there are hundreds of processes on the system in the first place. In such circumstances, it would be nice to let the computer do the work for you, and the top command makes that possible.