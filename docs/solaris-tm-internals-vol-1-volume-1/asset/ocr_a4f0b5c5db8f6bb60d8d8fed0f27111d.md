# A.6  Process and Dispatcher (Scheduler) Parameters

The parameters listed in Table A-8 relate to the process and scheduler subsystem in Solaris. For more information, refer to “The Kernel Process Table” on page 290”.

# **Table A-8**  *Process and Dispatcher (Scheduler) Parameters*

| Parameter | Default | Category | Description/Notes |
|---|---|---|---|
| `reserved_procs` | 5 | Limit | The number of process table slots reserved for system processes. |
| `maxpid` | 30,000 | Limit | Maximum value for a PID, and the maximum number of processes that can exist on the system at any one time. |
| `max_nprocs` | (10 + 16 * max-users) | Limit | Maximum number of process that can exist on the system. Will be set to maxpid if it is set to a value greater than maxpid. |
| `maxuprc` | max_nprocs_reserved_procs | Limit | Maximum number of processes a non-root user can create. |
| `noexec_user_stack` | 0 | Switch | If set to 1, stack pages are mapped noexec, providing protection against buffer overflow attacks. 64-bit Solaris 7 maps stack pages no-exec by default. |
| `rechoose_interval` | 3 | Tunable | Clock tick count for thread-to-processor affinity scheduling. The dispatcher attempts to place a thread on the same processor it last ran on, for optimal hardware cache hits. After rechoose_interval ticks, the next available processor is chosen. |
| `hires_tick` | 0 | Tunable | Default of 0 has the system generate 100 clock interrupts per second (10 ms interval). Setting this value to 1 results in a 1 ms interval (1000 clock interrupts per second). |

# A.7  STREAMS Parameters

Table A-9 lists tunable parameters available for the kernel STREAMS subsystem. STREAMS are not covered in this version of the book.