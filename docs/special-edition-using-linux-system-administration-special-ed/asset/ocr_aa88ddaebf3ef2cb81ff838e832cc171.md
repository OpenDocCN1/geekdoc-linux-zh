+   - The second line indicates the total number of processes plus the number sleeping, running, in a zombie state, and stopped.
+   - The third line indicates the percentage of CPU time spent in user mode, system mode, on tasks with a negative priority, and in an idle state.
+   - The fourth line displays memory usage information including total available memory, memory used, memory free, the amount of shared memory, and the amount of memory allocated to buffers.
+   - The fifth line displays information about swap space including total swap space, the amount of swap in use, and the amount of swap still available for use.

# The Role of Daemons

Daemons are special kinds of processes as explained earlier in the chapter. Unlike normal processes that are almost always associated with a controlling terminal, daemons do not have a controlling terminal. Look at the TTY column of the ps output shown earlier in the chapter for daemons such as inetd or init, and you will see there is no tty terminal associated with them.

In UNIX, daemons are a collection of specialized programs that perform particular system tasks. The following table lists common Linux daemons.

#### Table 8.3 Common Linux Daemons

| Daemon | Description |
|---|---|
| `init` | This is the great ancestor of all processes in the system. If init is killed or stops running for any reason, the system will reboot. |
| `kupdate` | This is the kernel updated process. It executes the sync system call every 30 seconds and writes current versions of all super blocks to disk. Keeping super blocks on disks up to date is very important, as it reduces the risk of file system damage in the event of a crash. |
| `kswapd` | This process is responsible for swapping pages out of main memory to disk and loading them back to memory when needed. |
| `inetd` | This is the Internet super-daemon. It starts up by reading its configuration file `/etc/inetd.conf`. This file tells it which ports `inetd` should listen to. It monitors these ports for incoming network connection requests. When a request arrives it spawns an instance of the appropriate daemon to handle that request. A more detailed discussion of this daemon can be found in Chapter 18, “General Security Issues.” |
| `crond` | This is the cron daemon. It wakes up periodically and runs jobs listed in `/var/spool/cron/crontab` directory. A detailed discussion of this daemon can be found in Chapter 7, “Scheduling Tasks.” |
| `named` | This is the internet name server daemon. It maps hostnames and IP addresses. A full discussion of this daemon is covered in Chapter 22, “DNS.” |