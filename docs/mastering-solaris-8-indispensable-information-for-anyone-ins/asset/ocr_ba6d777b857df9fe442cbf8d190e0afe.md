# FIGURE 15.1

The /usr/include/sys/procs.h file contains instructions for initiating system processes.

![](bbox=[0.3, 0.12, 0.94, 0.62])

A process exists in any one of five possible states:

**SIDL (idle)** The process is defined and is listed by the scheduler to run.

**SRUN (run)** The process is in the run queue.

**SSLEEP (sleep)** The process is temporarily suspended in the run queue. Typically, a process is in the sleep state when a system resource that it depends upon for execution is not available, such as data requiring I/O from disk.

**SSTOP (stopped)** An executing process is stopped. The parent process can stop a child process, or the process could be stopped by a signal from another process. To continue a stopped process, the system must receive a SIGCONT signal.