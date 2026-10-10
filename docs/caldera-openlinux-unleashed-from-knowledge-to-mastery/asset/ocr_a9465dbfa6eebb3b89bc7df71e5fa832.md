+   * SIGILL  The “illegal instruction” signal. You don’t usually send `SIGILL` to a process; the kernel sends it if the process executes an illegal instruction (that is, the program is buggy).

+   * SIGIOT  The “I/O trap” signal. `SIGIOT` causes a core dump and program termination. The Standard C function `abort` sends a process with this signal.

+   * SIGBUS  The “bus error” signal, causing core dump and termination. Symptomatic of a buggy program.

+   * SIGFPE  The “floating-point exception” signal, causing core dump and termination. Symptomatic of a buggy program.

+   * SIGSEGV  The “segmentation fault” signal, sent when a process tries to access memory in an illegal manner. Causes a core dump and termination.

+   * SIGKILL  The “kill” signal. `SIGKILL` is the nuclear bomb of UNIX. Although most other signals can be intercepted by a process, the KILL signal cannot. SIGKILL is the most drastic (but reliable) way to terminate a process.

+   * SIGSTOP  The “stop” signal. `SIGSTOP` stops (but does not terminate) a process. You can achieve much the same thing for a running process by typing the stop key, usually Ctrl+Z.

+   * SIGCONT  The “continue” signal. `SIGCONT` resumes a stopped process.

For more details about kill, see `kill(1)`. Note that if you are using bash or ksh, `kill` is actually built into the shell. However, it operates similarly to the non–built-in kill program (found in `/bin/kill`).

# ## Monitoring Processes: top

The top command shows a snapshot of the running processes on the system, updated every few seconds. Once top is running, you can use the following keys:

+   * Spacebar—Update the display.

+   * F—Add or remove columns from the display. You can display 26 pieces of information for each process; this screen lets you choose which pieces of information you want to see.

+   * I—Toggle the display of idle processes. Normally, idle processes are displayed (unless you start top with the -l option).

+   * S—Set the delay in seconds between updates. You can also use the command-line option -d n where n is the delay.

+   * Q—Quit.