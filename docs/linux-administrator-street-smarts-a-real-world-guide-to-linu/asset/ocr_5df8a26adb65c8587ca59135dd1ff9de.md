time; it's only when CPU time becomes scarce (that is, when the load average climbs above 1) that process priorities become important.

Ordinarily, if two processes are competing for CPU time and both have the same priority, the kernel divides CPU time equally between them. The effect of changing the priority of one process is to alter the proportion of CPU time given to the two processes. If the process priorities differ by just 1 (say, nice values of 0 and 1), they'll still get close to equal amounts of time, but the process with a higher nice value will get slightly less CPU time. As the difference in nice values increases, so does the proportion of CPU time given to the two processes. A process with a nice value of 19 is given so little priority that it runs only when no other process is demanding CPU time. This makes a nice value of 19 appealing for processes that are CPU intensive but not critical to overall system operation, such as distributed computing projects like Folding@Home (http://folding.stanford.edu).

Intermediate nice values, such as 10, are useful when you want a job to run at a reasonable pace but not interfere too much with other processes. For instance, you might run a program compilation at a nice value of 10 if you or other users are doing work on the system while the compile is running.

Most user programs, such as Web browsers, word processors, and shells, spend most of their time idling, waiting for keyboard input. Even if you're typing furiously, the program takes far less time to process your keystrokes than you take making them. Thus, if you're running, say, a word processor and a CPU-intensive ray-tracing program, running the ray-tracing program with a reduced priority won't rob it of much CPU time; however, when your finger dies hit a key in the word processor, that action will take priority, so you'll see less of a performance drop in the word processor than you'd see if you ran the ray tracer at normal priority.

# ### Launching Programs with Specified Priorities

To launch a program with reduced priority, type nice followed by the name of the program:

```
$ nice glxgears
```

This command launches the glxgears program with a nice value of 10 (the default). Alternatively, you can specify a particular value by using the -n value, --adjustment=value, or -value options before the command you're running with nice. For instance, the following three commands are all equivalent to the previous one:

```
$ nice -n 10 glxgears
$ nice --adjustment=10 glxgears
$ nice -10 glxgears
```

![](bbox=[0.12, 0.81, 0.2, 0.89])

The -value form of adjustment makes a confusing situation worse; it looks like you're specifying a negative value, but in fact the dash just indicates that the following number is an option to nice.