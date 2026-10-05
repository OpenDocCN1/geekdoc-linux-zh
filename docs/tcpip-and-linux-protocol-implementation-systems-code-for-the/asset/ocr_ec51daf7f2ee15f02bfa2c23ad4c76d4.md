# Protocol Implementation Framework 111

| Process a | Process b |
| --- | --- |
| Resource owned: x | y |
| Resource required: y | x |
| | 
 Time advances down the page | |

**Figure 5.2** Deadlock.

| Process a | Process b | Process c |
| --- | --- | --- |
| Resources owned: x | y | wants x and/or y |
| y | y | |
| x | x | |
| Time advances | | |

**Figure 5.3** Livelock.

Linux is now pretty much fully symmetric multiprocessor-capable. Atomic access to shared data must be protected across processes, since any layer (e.g., driver interrupt, software interrupt, system call handler) may run on any processor.

In Chapter 2, we discussed the mutual exclusion support that this requires, the technique called a spinlock. For input and output, this is a relatively simple (localized) change to all the communications code that has happened in the last few years of evolution of the Linux kernel, so that we have greatly enhanced performance in multiprocessor hardware systems. The remaining area for performance enhancement is in SMP forwarding, but this is a topic for future research at the moment, as mentioned before.