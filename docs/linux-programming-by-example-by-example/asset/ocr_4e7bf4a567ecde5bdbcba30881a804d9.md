# Additional Process Information

More information than just process, user, and group IDs is available about processes, such as their resource usage and execution times. Note that I wrote execution *times*, not *time*. This is because the Linux kernel maintains three separate time values for processes, as follows:

+   • *Wall clock time* is elapsed time.

+   • *User CPU time* is the amount of time the processor spends executing user mode (non-kernel mode) code.

+   • *System CPU time* is the amount of time spent executing kernel code.

> • The difference between user mode and kernel mode is discussed in "What Is A System Call?" page 120.

You can obtain this information by calling `times` or `getrusage`. A process's resource usage, however, can be obtained only from the `getrusage` call. These resources are all concerned with memory-access statistics. This section discusses obtaining timing information first, and then covers resource usage.

> **TIP**
> Which call, `times` or `getrusage`, should you use to obtain timing information? Well, Linux has inherited functionality from both BSD and SVR4 UNIX, and they both have both functions. POSIX, a standard Linux attempts to follow, only mandates *times*. However, `getrusage` gives programmers a more complete picture of a process's resource usage, at least in theory. It is theoretical because Linux (as of version 2.2.10) implements only five of the sixteen resources defined in the *rusage* structure. Finally, the timing information *times* returns is more finely grained than that returned by *getrusage*. So, if you only need timing information or want to adhere to the POSIX standard, use `times`. If you do not care about POSIX compliance or if you need the additional information provided by `getrusage`, use it instead.

# Process Timing

The `times` function is prototyped in <`sys`/`times.h`> as follows:

```
clock_t times(struct tms *buf);
```

*times* returns the number of clock ticks that have elapsed since the system was brought up, also known as wall clock time. *buf* is a pointer to a *tms* structure that stores the current process *times*.

# *Example*

![](bbox=[0.04, 0.75, 0.1, 0.79])

# Example

This program uses the *system* function to execute an external command, and then uses the *times* call to print the resulting timing information.

```
/* resusg1.c - Get process times and resource usage
 */
```