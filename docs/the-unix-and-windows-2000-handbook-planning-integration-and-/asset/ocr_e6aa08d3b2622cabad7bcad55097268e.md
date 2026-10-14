# ps

This is the UNIX equivalent of the pmon command in Windows 2000. ps provides a snapshot of processes currently running on the system, and is probably one of the most utilized commands on UNIX systems. Figure 14.7 is the output of ps with the -e (every process now running) and -l (generate long listing) switches.

Column S indicates the state of the process (definitions in Table 14.2). Column UID contains the effective user ID of the process and is how you identify the guilty party. Column PID contains the process ID of the process and is required to kill or renice the process. Column NI contains the nice value. Column SZ contains the size in pages of the process’ image in memory. Column TIME is the cumulative execution time of the process and column CMD is the command name up to 80 characters. The other columns can be ignored with respect to performance monitoring.

> ps—Provides a snapshot of processes currently running on the system, and is probably one of the most utilized commands on UNIX systems. This is the UNIX equivalent of the pmon command in Windows 2000.

![](bbox=[0.052, 0.529, 0.879, 0.932])

Figure 14.7  ps piped to more on Solaris 2.6.