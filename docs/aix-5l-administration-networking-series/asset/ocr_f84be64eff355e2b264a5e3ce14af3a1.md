+   - Resource utilzation
+   - Process state

# Displaying Process Attributes

The **ps** command is your friend when you need to look at processes in the system. The **ps** command options are many, and as with many AIX commands, you can use either System V or BSD command switches. The System V **ps** command is used when the command-line arguments are preceded by the hyphen character (-); otherwise, the BSD format is used. You can also use SMIT and the Web-Based System Manager to invoke **ps**, but you may find using **ps** from the command line to be faster.

The **ps -eLk SYSV** command displays processes using the following format:

F S  UID  PID  PPID  C  PRI  NI  ADDR  SZ   WCHAN  TTY     TIME     CMD
103 A 0      0     0    120  16    --    2412  12         -  6:51  swapper
200003 A 0    1     0    60   20  142a  836          -  1:13  init
103 A 0      516   0    120  255   --  2613  8       *    775:05 wait
103 A 0      1032  0    0    37    --  1028  64         -  21:01 g11
103 A 0      129   0    0    16    --  1229  16   6ae819  -    0:00 lmched
46201 A 0    2608  0    0    60   20  2472  16   0c46b3  0:00 lvmbd
40401 A 0    2672  1    0    60   20  134c  572 14b774  0:00 kerdsmon
240001 A 0   2919   1    0    60   20  1b4d  780  -          0:00 rcmsmt
40103 A 0    3128  1    0    39    --  1f2f  16         -  0:00 loServer
241001 A 0   3392   1    0    60   20  663  320 309eb298  5:06 synccd

The **ps auxww** BSD command displays processes using the following format:

USER    PID   %CPU %MEM  SZ    RSS   TTY  STAT   STIME      TIME     COMMAND
root    516    98.8  8.0   8   10520   -  A     Feb 04   788:38 wait
root   22036    0.6   1.0   1512  1424   -  A     4:24:01    0:18   /usr/db2/bin/db2terr
root    1032    0.2  8.0    64  10576   -  A     Feb 04   21:03 g11
root       1    0.1  8.0    12  10524   -  A     Feb 04   6:51 swapper
root    3392    0.1  0.0    320  240     -  A     Feb 04   5:06 /usr/lib/sysv/rc/synccd 60
root       1    0.0  0.0     836  288    -  A     Feb 04   1:13 /etc/init
root   13936    0.0  0.0   1372  344     -  A     Feb 04   1:00 /usr/db2/bin/db2login
root   17098    0.0  0.0   2484  2016  pty8/A  A   Feb 04   0:54  dswm
root     5160    0.0  1.0   1368  1212   -  A     Feb 04   0:27 /usr/sbin/asmcpd

The COMMAND and CMD columns represent the program being run in the process address space. You may have noticed the COMMAND with PID number (516) from the preceding **ps auxww** command output. This PID is always the **first wait** (or **kproc**) process. The **wait** process collects CPU time when there are no threads to run for a given time slice. This is no cause for alarm. A **wait** process is assigned to each CPU so that the scheduler has somewhere to put the idle time. Since the AIX operating system must always be doing *something*, if the CPU is idle the **wait** process just keeps the clock ticking. The **wait** process is the AIX 5L replacement for the **kproc** process that is seen in the process table of AIX 4.3.3 and earlier.