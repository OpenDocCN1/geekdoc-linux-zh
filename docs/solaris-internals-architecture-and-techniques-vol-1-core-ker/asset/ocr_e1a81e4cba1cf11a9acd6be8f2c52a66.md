# Table 8-4 Irusage Fields (Continued)

| Field | Description |
|---|---|n| nswap | Number of times the LWP was swapped out. Incremented in the LWP swapout() code. |
| inblock | Number of input blocks. Incremented in the kernel block I/O subsystem (bio.c) for device reads. |\| outblock | Number of output blocks. As above, incremented in bio.c for device writes. | msgsnd | STREAMS messages sent. Incremented in the STREAMS common code for putmsg(). |
| msgrcv | STREAMS messages received. Incremented in the STREAMS common code for getmsg(). |
| nsignals | Number of signals received. Incremented in the kernel psig() code, where the LWP is set up to run the signal handler. |
| nvcw | Number of voluntary context switches. Incremented when LWP blocks (is put to sleep), waiting for an I/O or synchronization primitive. |
| nivscw | Number of involuntary context switches. Incremented when an LWP is context-switched because it uses its allotted time quantum or is preempted by a higher-priority kthread. |
| sysc | Number of system calls. Incremented in the system call trap handler. |
| ioch | Characters read and write. Incremented in the read/write system call code. |

The resource utilization counters do not require enabling microstate accounting for the process or LWP. They are accessible through the usage structure maintained by procs, where /proc/<PID>/usage represents the process level usage and /proc/<PID>/lwp/<LWP_ID>/lwusage represents the per-LWP usage data. See the code in Appendix C, "A Sample Procs Utility"

Within the process, the operating system maintains a high-resolution timestamp that marks process start and terminate times. A p_start field, the start time, is set in the kernel fork() when the process is created, and the process termination time, p_term, is set in the kernel exit() code. Start and termination times are also maintained in the LWP where microstate accounting is enabled. The associated process p_real field contains a sum of the LWP's elapsed time, from the start and termination times.

The system uses an internal gethrtime() routine, get_high_resolution_time (there is an equivalent gethrtime(3C) API). When get_high_resolution_time is called, it returns a 64-bit value expressed in nanoseconds. The value is not related to current time and is thus useful when used in conjunction with a subsequent call to gethrtime(). In case,