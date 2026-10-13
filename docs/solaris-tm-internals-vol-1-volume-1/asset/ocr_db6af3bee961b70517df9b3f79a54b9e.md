+   - Updates the `lbolt` counter. `lbolt` counts the number of clock ticks since boot.
+   - Processes the kernel callout table (described in the next section).
+   - If on a one-second interval, calculates kernel swap parameters (free, reserved, and allocated swap) and adjusts systemwide run queue size and swap queue size.

Once the clock interrupt handling is completed, the clock interrupt thread is context-switched off the processor, and the thread that was executing when the interrupt occurred resumes.

# 2.6.1 Process Execution Time Statistics

The CPU usage work and thread tick processing is done on a per-CPU basis; the code loops through the list of online processors and does the work for each CPU. Usage information is maintained in the `cpu[]` array in each CPU’s `sysinfo` structure. The four-member `cpu[]` array stores an integer value, one for each of USER, SYSTEM, IDLE, and WAIT—the four possible states that the CPU will be in. A CPU in the QUEUED state is charged with idle time. A CPU running an interrupt thread is charged with system time. A CPU running its idle thread is charged with idle time unless the `cpu_syswait.iowait` value is set; in that case, the CPU is charged with I/O time.

`cpu_syswait.iowait` is set in the `biowait()` routine, which is called from the file system support code when a buffered I/O is issued (see Part III, The Solaris File I/O System for specifics on buffered I/O). `biowait()` is also called from the disk drivers in the kernel; thus, with I/O time reflects I/O through the file system as well as raw disk I/O; wait I/O reflects disk I/O only, and network I/O is not reflected. The algorithm for calculating wait I/O was flawed in releases prior to Solaris 7, and CPUs that were idle may be charged incorrectly with wait I/O time. Finally, if a thread that is not idle is executing on a CPU, the state of the thread is checked to determine if the CPU should be charged with user time (the thread is executing in user mode) or system time.

The last bullet item in the previous section indicates that some of the clock interrupt processing is not done in every clock interrupt (100 times a second), but rather at one-second intervals. For the services indicated, one-second granularity is sufficient.

Tick processing is done for each kernel thread (if that thread is not an interrupt handler or an operating system kernel thread) running on a CPU. Each kernel thread maintains a `t_pctcpu` (percent of CPU time) and `t_lbolt` value, where `t_pctcpu` is used for per-thread usage information (e.g., accounting) and `t_lbolt` provides a point of reference for tick processing. The kernel determines whether it