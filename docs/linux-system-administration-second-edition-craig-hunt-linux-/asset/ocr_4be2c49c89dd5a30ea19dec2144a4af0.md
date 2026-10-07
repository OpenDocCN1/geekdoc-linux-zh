Looking at the process group ID (PGID), we can see that kflushd, kupdate, kp1od, and kswapd all belong to the bin group. The session ID (SID) that follows tells us that these processes belong to the same session. The PGID and the SID are set to the PID of the calling process, so we know that these processes were called by the init process.

The TTY field tells where the process is running. The files started up as part of the initialization process typically have a ? in this field since they are not tty–specific. The processes specific to a tty list that tty number (or, in the case of a remote login, a pts number).

> **Tip** A tty is a login session connected to the standard output pipe; that is, it is local to the CPU. Linux has six terminals (ttys) defined by default. A pts entry indicates a login by telnet or xterm. pts/0 is the first such login.

The TIME column shows the total amount of system (CPU) time used by the process so far; this is not equivalent to the amount of clock time since the process started, because we are on a multitasking system.

The process status codes (STAT) can be interpreted using the following information as taken directly from the ps man page:

+   - D uninterruptible sleep (usually I/O)
- R runnable (on run queue)
- S sleeping
- T traced or stopped
- Z a defunct ("zombie") process
- W has no resident pages
- < high-priority process
- N low-priority task
- L has pages locked into memory (for real-time and custom I/O)

We’ve hardly scratched the surface of the ps command, but we will revisit it when we discuss managing processes a little later in this chapter. First we will examine the initialization process used by Linux. Some of the details vary from distribution to distribution; this discussion uses the Red Hat process as a model, pointing out differences in other distributions where appropriate.

# The init Process

The most important process in a Linux system is init. The first process started on a Linux system, it is assigned the PID 1. The init process is owned by the root user and has a PPID of 0.

The last thing the kernel does when it boots is to start the init process. The init process controls the rest of the boot process by checking and mounting the filesystems, starting the necessary daemons, and doing whatever else it has been configured to do. Chapter 3 discussed how to configure the init process.

When a parent process dies before all of its child processes have died, the remaining child processes are said to be *orphan* processes. These processes are required to have a parent process, so the init process adopts the orphan processes until they, too, are completed or killed.

Listing 7.5 illustrates what happens when a user logs in to your system. Earlier in the chapter we saw the output from the ps –axj command. This time we use the –aux parameter set, which displays the user who owns the process, the process ID, the percentage of the CPU that this process is consuming, the amount of memory that this process is consuming, and the time the process started.