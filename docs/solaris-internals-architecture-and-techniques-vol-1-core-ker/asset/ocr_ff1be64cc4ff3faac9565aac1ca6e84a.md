# 8.2.4 The Kernel Thread (kthread)

The kernel thread is the entity that actually gets on a dispatch queue and scheduled. This fact is probably the most salient departure from traditional UNIX implementations, where processes maintain a priority and processes are put on run queues and scheduled. It's the kthread, not the process, that is assigned a scheduling class and priority. You can examine this on a running system using the -L and -c flags to the ps(1) command. The columns in the ps(1) output below provide the process (PID), the LWP number within the process (LWP), the scheduling class the LWP is in (CLS), and the priority (PRI).

| ps -eL PID LWP TTY TIME CMD |
|---|---|---|---||
| 0 | 1 | | 0:01 sched |
| 1 | 1 | | 0:00 init |
| 2 | 1 | | 0:00 pageout |
| 3 | 1 | | 1:40 fsflush |
| 235 | 1 | | 0:00 sendmail |
| 260 | 1 | | 0:00 void |
| 260 | 2 | | 0:00 void |
| 260 | 3 | | 0:00 void |
| 260 | 4 | | 0:00 void |
| 260 | 5 | | 0:00 sac |
| 319 | 1 | | 0:00 in_route |
| 121 | 1 | | 0:00 keyserv |
| 133 | 2 | | 0:00 keyserv |
| 133 | 3 | | 0:00 keyserv |
| 133 | 6 | | 0:00 upd |
| 300 | 1 | | 0:00 rpcbind |
| 131 | 1 | | 0:00 inetd |
| 158 | 1 | | 0:00 syslog |
| 184 | 1 | | 0:00 syslog |
| 184 | 2 | | 0:00 syslog |
| 184 | 3 | | 0:00 syslog |
| 184 | 4 | | 0:00 syslog |
| 184 | 5 | | 0:00 syslog |

It is interesting to note that the output indicates that the LWP has a priority and scheduling class, when technically it's the kthread associated with the LWP that actually maintains this information.

The kernel thread structure is defined in /usr/include/sys/thread.h. The significant fields in the kthread include the following:

+   - t link — Pointer to a kthread structure. Linked list support, links the kthread with other threads on the same queue: dispatch, sleep, queue, and free queue.
- t_stack — Kernel stack pointer (address).
- t bound_cpu — Pointer to a CPU structure. Data to manage binding to a processor, and data to support a processor set.
- t_affinitycnt — Maintains CPU affinity (loose coupling to a specific processor, best effort to keep a thread on the same CPU).