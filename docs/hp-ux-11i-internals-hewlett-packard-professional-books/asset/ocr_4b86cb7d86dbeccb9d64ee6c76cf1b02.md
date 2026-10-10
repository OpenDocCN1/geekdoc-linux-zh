To convert an internal priority to an external POSIX priority (the priority number you would pass as an argument in the rt sched() system call or rt sched line-mode command):

> External-POSIX-Priority = (MAX_RT SCHED_PRI - 1) - Internal-priority

To convert an external POSIX priority to an internal priority:

> Internal-Priority = (MAX_RT SCHED_PRI - 1) - External-POSIX-priority

Next, let's examine the scheduling schemes.

# SCHED_TIMESHAKE and SCHED_NOAGE

The classic UNIX scheduler is implemented in HP-UX as SCHED_TIMESHAKE. This policy has two additional aliases: SCHED_OTHER and SCHED_HPOX. In Figure 5-13, we illustrate the basics of the timeshare scheduler and position it with respect to the overall priority system.

![](bbox=[0.1, 0.41, 0.9, 0.55])

| |  | HP-UX Timeshare Priorities | 32 queues, 4 priorities/queue |  | 252-255 |
|---|---|---|---|---|---|
| 128-131 |  |  |  |  | 255 |
|  |  | System, Timeshare |  | PUSER | User, Timeshare |
| 128 | Delay Signals 153 | 154 Wake for Signals 177 |  |  |  |
| PZERO |  |  |  |  |  |

# Figure 5-13 Thread Priorities

This scheduling policy consists of 32 run queues. Each queue contains four sequential priority values. The strongest queue handles threads with priorities between 128 and 131, while the weakest handles those between 252 and 255. The four priorities per queue is part of the legacy left by the early UNIX development work done on an older Digital Equipment Corp. hardware platform. The system was set up to handle 32 unique queues; this number was carried through in the UNIX kernel design. When it was decided to increase the priority range to an 8-bit value (0