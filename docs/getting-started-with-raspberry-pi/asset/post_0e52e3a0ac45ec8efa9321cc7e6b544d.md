
Init finally spawns terminals on virtual consoles. You can now log in.

## Kernel Mode and User Mode

Some operating systems, such as MS-DOS, always execute in a single CPU mode, but UNIX-like operating systems use dual modes to effectively implement time-sharing. On a Linux machine, the CPU is either in a trusted *kernel mode* or in a restricted *user mode*. All user processes execute in user mode, whereas the kernel itself executes in kernel mode.

Kernel mode code has unrestricted access to the entire processor instruction set and to the full memory and I/O space. If a user mode process needs these privileges, it has to channel requests through device drivers or other kernel mode code via system calls. User mode code is allowed to page fault, however, whereas kernel mode code isn't.

In 2.4 and earlier kernels, only user mode processes could be context switched out and replaced by other processes. Kernel mode code could monopolize the processor until either:

-   * It voluntarily relinquished the CPU.
-   * An interrupt or an exception occurred.

With the introduction of kernel preemption in the 2.6 release, most kernel mode code can also be context switched.

## Process Context and Interrupt Context

The kernel accomplishes useful work using a combination of process contexts and interrupt contexts. Kernel code that services system calls issued by user applications runs on behalf of the corresponding application processes and is said to execute in process context. Interrupt handlers, on the other hand, run asynchronously in interrupt context. Process contexts are not tied to any interrupt context and vice versa.

Kernel code running in process context is *preemptible*. An interrupt context, however, always runs to completion and is not *preemptible*. Because of this, there are restrictions on what can be done from interrupt context. Code executing from interrupt context cannot do the following:

-   Go to sleep or relinquish the processor
-   Acquire a mutex
-   Perform time-consuming tasks
-   Access user space virtual memory

Look at section "Interrupt Handling" in Chapter 4 for a full discussion of the interrupt context.

## Kernel Timers

The working of many parts of the kernel is critically dependent on the passage of time. The Linux kernel makes use of different timers provided by the hardware to provide time-dependent services such as busy-waiting and sleep-waiting. The processor wastes cycles while it busy-waits but relinquishes the CPU when it sleep-waits. Naturally, the former is done only when the latter is not feasible. The kernel also facilitates scheduling of functions that desire to run after a specified time duration has elapsed.

Let's first discuss the semantics of some important kernel timer variables such as `jiffies`, `HZ`, and `xtime`. Next, let's measure execution times on a Pentium-based system using the Pentium *Time Stamp Counter* (TSC). Let's also see how Linux uses the *Real Time Clock* (RTC).

### HZ and Jiffies

System timers interrupt the processor (or “pop”) at programmable frequencies. This frequency, or the number of timer ticks per second, is contained in the kernel variable `HZ`. Choosing a value for `HZ` is a trade-off. A large `HZ` results in finer timer granularity, and hence better scheduling resolution. However, bigger values of `HZ` also result in larger overhead and higher power consumption, because more cycles are burnt in the timer interrupt context.

The value of `HZ` is architecture-dependent. On x86 systems, `HZ` used to be set to 100 in 2.4 kernels by default. With 2.6, this value changed to 1000, but with 2.6.13, it was lowered to 250. On ARM-based platforms, 2.6 kernels set `HZ` to 100. With current kernels, you can choose a value for `HZ` at build time through the configuration menu. The default setting for this option depends on your distribution.

The 2.6.21 kernel introduced support for a tickless kernel (`CONFIG_NO_HZ`), which dynamically triggers timer interrupts depending on system load. The tickless system implementation is outside the scope of this chapter.

`jiffies` holds the number of times the system timer has popped since the system booted. The kernel increments the `jiffies` variable, `HZ` times every second. Thus, on a kernel with a `HZ` value of 100, a jiffy is a 10-millisecond duration, whereas on a kernel with `HZ` set to 1000, a jiffy is only 1-millisecond long.

To better understand `HZ` and `jiffies`, consider the following code snippet from the IDE driver (*drivers/ide/ide.c*) that polls disk drives for busy status:

```c
unsigned long timeout = jiffies + (3*HZ);
while (hwproup->busy) {
    /* ... */
    if (time_after(jiffies, timeout)) {
        return -EBUSY;
    }
    /* ... */
}
return SUCCESS;
```

The preceding code returns `SUCCESS` if the busy condition gets cleared in less than 3 seconds, and `-EBUSY` otherwise. `3*HZ` is the number of `jiffies` present in 3 seconds. The calculated timeout, `(jiffies + 3*HZ)`, is thus the new value of `jiffies` after the 3-second timeout elapses. The `time_after()` macro compares the current value of `jiffies` with the requested timeout, taking care to account for wraparound due to overflows. Related functions available for doing similar comparisons are `time_before()`, `time_before_eq()`, and `time_after_eq()`.

`jiffies` is defined as `volatile`, which asks the compiler not to optimize access to the variable. This ensures that `jiffies`, which is updated by the timer interrupt handler during each tick, is reread during each pass through the loop.

For the reverse conversion from `jiffies` to seconds, take a look at this snippet from the USB host controller driver, `drivers/usb/host/ehci-sched.c`:

```c
if (stream->rescheduled) {
    ehci_info(ehci, "ep%d=iso rescheduled %u times in %lu "
               "seconds\n", stream->bEndpointAddress, is_in? "in":
               "out", stream->rescheduled,
               ((jiffies - stream->start)/HZ));
}
```

The preceding debug statement calculates the amount of time in seconds within which this USB endpoint stream (we discuss USB in Chapter 11, “Universal Serial Bus”) was rescheduled `stream->rescheduled` times. (`jiffies-stream->start`) is the number of `jiffies` that elapsed since the rescheduling started. The division by `HZ` converts that value into seconds.

The 32-bit `jiffies` variable overflows in approximately 50 days, assuming a `HZ` value of 1000. Because system uptimes can be many times that duration, the kernel provides a variable called `jiffies_64` to hold 64-bit `(u64)` `jiffies`. The linker positions `jiffies_64` such that its bottom 32 bits collocate with `jiffies`. On 32-bit machines, the compiler needs two instructions to assign one u64 variable to another, so reading `jiffies_64` is not atomic. To get around this problem, the kernel provides a function, `get_jiffies_64()`. Look at `cpufreq_stats_update()` defined in `drivers/cpufreq/cpufreq_stats.c` for a usage example.

### Long Delays

In kernel terms, delays in the order of `jiffies` are considered long durations. A possible, but nonoptimal, way to accomplish long delays is by busy-looping. A function that busy-waits has a dog-in-the-manager attitude. It neither uses the processor for doing useful work nor lets others use it. The following code hogs the processor for 1 second:

```c
unsigned long timeout = jiffies + HZ;
while (time_before(jiffies, timeout)) continue;
```

A better approach is to sleep-wait, instead of busy-wait. Your code yields the processor to others, while waiting for the time delay to elapse. This is done using `schedule_timeout()`:

```c
unsigned long timeout = jiffies + HZ;
schedule_timeout(timeout); /* Allow other parts of the
                    kernel to run */
```

The delay guarantee is only on the lower bound of the timeout. Whether from kernel space or from user space, it’s difficult to get more precise control over timeouts than the granularity of `HZ` because process time slices are updated by the kernel scheduler only during timer ticks. Also, even if your process is scheduled to run after the
