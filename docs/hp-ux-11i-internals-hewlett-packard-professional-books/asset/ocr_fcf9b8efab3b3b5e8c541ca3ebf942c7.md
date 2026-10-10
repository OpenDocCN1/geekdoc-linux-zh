# **POSIX Real-Time Scheduler**

The last of the three main schedulers—and the newest—is the POSIX real-time scheduler, Figure 5-15 illustrates its position in the priority continuum. This scheduler features three different policies: **SCHED_FIFO, SCHED_RR, and SCHED_RR2**.

![](bbox=[0.18, 0.23, 0.82, 0.39])

**Figure 5-15 SCHED_RTPRIO**

When the POSIX committee first approached the creation of a UNIX real-time scheduler specification, it requested several key features:

+   - The POSIX scheduler would feature up to 512 single-priority run queues.
+   - The number of queues would be configurable between 32 and 512.
+   - The weakest priority would be 1 and the strongest 512.
+   - Each thread assigned to a run queue would have a choice of three scheduling policies among other threads with which it shared a queue: FIFO, RR, and RR2.
+   - The POSIX run queues would be systemwide and not tied to a specific processor. When a POSIX queue had an active, runnable thread and it was the strongest queue, it would schedule the thread to run on the first available processor (unless the thread itself had expressed a specific processor affinity).

The implementation of these design goals presented its own set of challenges, as we previously mentioned. To understand how these features have been implemented in the HP-UX kernel, let's break them down.

# **Sizing the POSIX Queues**

The sizing of the POSIX queue is controlled by a tunable kernel parameter, *rtsched_npri*. The minimum supported value is **RTSCHED_NUMPRI_FLOOR**, or 32, and the maximum is **RTSCHED_NUMPRI_CEILING**, or 512. Most systems simply leave this parameter at its default value of 32. Once this count is set, the kernel builds the POSIX run queues. The POSIX run queue is considered to be global, but it should be noted that on large