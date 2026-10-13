
also fork/execs a child, *ccc3*. So, we end up with a reasonably realistic process hierarchy that we can use for illustration.

![](img/220ae4af07df2fe8e5be69d27f885d1b_318_0.png)

**Figure 8.8** *Process Lineage Pointers*

In Figure 8.8, pointers without connecting lines are NULL. The linked pointers can be summarized as follows. The parent and child pointers are (we hope) straightforward. The *bd* process parent pointer links to the shell that spawned it (not shown), the child pointer links to *c3*, the last child created (chronologically), nextofkin links to the parent, and orphan links to the last child created, *c3*. The three children, *c1*, *c2*, and *c3*, of the *bd* process link to each other through the sibling and psibling pointers, forming a linked list of all the children spawned by the same parent (*bd*). The `nextofkin` pointer in all three child processes links to the parent, *bd*.

The *cc2*, *cc3*, and *ccc3* processes have no siblings; thus, the `sibling` pointers are NULL. They link back to the parent through the `parent` and `nextofkin` pointers. And of course, the parent/child links between the *cc3* and *ccc3* processes round out the picture.

The way the picture changes if a process dies is due in part to how the code is constructed. In this example, the *bd* process was blocking in a `waitpid(2)` call, waiting on the PID of the *c3* process. We killed process *c3*, which resulted in *bd* and *c3* both terminating, leaving *c1*, *c2*, *cc2*, and *ccc3*. The parent and `nextofkin` pointers in *c1*, *c2*, and *ccc3* linked to the `init` process, which inherits orphan processes. The `sibling` pointers in *c1* and *c2* changed, where `sibling` in *c1* linked to *c2*, and `psibling` in *c2* linked back to *c1*.

Additional pointers maintained in the proc structure include the following:

- **p_sessp** — Pointer to a session structure, which contains information for managing the process’s control terminal. See “Sessions and Process Groups” on page 342.
- **p_pidp** — Pointer to a `pid` structure, for process ID (PID) information. The process’s actual PID is stored in one of the fields in the `pid` structure.
- **p_pgidp** — Another `pid` structure pointer, for process group information (process group ID).

The Solaris kernel maintains a data structure for managing PIDs and process group IDs (Figure 8.9).

![](img/220ae4af07df2fe8e5be69d27f885d1b_319_0.png)

The first 4 bytes of the PID structure store 2 status bits, `pid_prinactive` and `pid_pgorphaned`, followed by 6 pad bits (unused bits) and 24 bits to store the slot number of the `/proc` table entry for the process, `pid_prslot`. Since we use 24 bits to store the unique `/proc` table entry for processes, we have a limit of 16 million possible `/proc` table entries. This limit will never actually be reached in Solaris versions up to and including Solaris 7 because the kernel defines a MAXPID value of 30,000. The limit of 30,000 processes is imposed by the use of a 2-byte data type in the `utmp` structure.

The kernel maintains `/var/adm/utmp` and `/var/adm/wtmp` files for the storage of user information used by the `who(1)`, `write(1)`, and `login(1)` commands (the accounting software and commands use `utmp` and `wtmp` as well). The PID data is maintained in a signed short data type, which has a maximum value of 32,000. This “limit” should in no way be construed as a problem; 30,000 is a great many processes and our last install test today had nowhere near that many processes running. See “The Kernel Process Table” on page 290 for a description of how the actual system process limits are established.

The PID structure links to other PID structures in the kernel through `pid_link`, which maintains a hashed list of active PIDs in the kernel, and `pid_pglink`, which links back to the process structure. Finally, the `prinactive` bit flags the structure as being free or used, and `pgorphaned` indicates whether the process is orphaned (the parent has exited or died—orphaned processes are adopted by the `init` process).

Several condition variables are maintained in the proc structure. Condition variables are a kernel synchronization mechanism used to notify a process or thread if a specific event, such as the completion of an I/O, has occurred. Condition variables are used in the Solaris environment to implement sleep and wakeup. One such condition variable is `p_holdlwps`, a special condition variable for holding process LWPs. In a `fork()`, the LWPs must be suspended at some point so their kernel stacks can be cloned for the new process.

In the process structure, the kernel maintains time totals that reflect the amount of user time and system time the process accumulated, as well as summations for all the child processes’ system time and user time. The child information is summed when a child process exits. The `p_utime` and `p_stime` fields maintain the process’s user and system time, respectively; the `p_cutime` and `p_cstime` fields maintain the child process’s user and system time.

The process maintains several bits of information on LWPs and kernel threads, including a total of all LWPs linked to the process (`p_lwpnt`), and all LWPs created, `p_lwptotal`. The latter may be different from `p_lwpnt` because the kernel may have allocated LWPs to the process from the systemwide pool. Such LWPs will not have been explicitly created by the process. Counters are maintained for the number of blocked LWPs (`p_lwpblocked`), runnable LWPs (`p_lwprcnt`), and zombie LWPs (`p_zombcnt`). A pointer rooted in the proc structure references a linked list of kernel threads (`p_tlist`) and a linked list of zombie threads (`p_zomblist`). (A zombie process is a process that has exited but whose parent process did not issue a wait call to retrieve the exit status.)

The remaining members of the process structure can be grouped into several categories. Per-process signal handling support involves linking to signal queue structures, supporting the signal mask and signal posting structures. The Solaris signal model has undergone significant work to support the multithreaded architecture and is discussed beginning on page 330. Support for the /proc file system requires the inclusion of various pointers and data types in the proc structure. Also, the Solaris kernel includes a facility called Doors, which provides a fast cross-process call interface for procedure calling.

Process-level resource usage and microstate accounting information are maintained within the process structure, as well as on a per-LWP basis. We discuss the details in “The Kernel Process Table” on page 290.

Process profiling is supported by the inclusion of a prof structure (_prof) and is enabled when the program is compiled (i.e., before it becomes a “process”). During the execution of the process, process profiling gathers statistical data that tells the programmer which routines the process was spending time executing in and how much time was spent in each function relative to the total execution time of the process.

You can use the `/etc/crash(1M)` utility to examine the contents of a proc structure on a running system. First, use the `p` function with no arguments to dump the process table. Determine the process table slot of the process you’re interested in, then use `p -f slot_number` to dump the contents. To save space, we’re showing a partial listing of the process table dump and structure.

```text
# ps
  PID TTY        TIME CMD
24676 pts/6      0:00 sh
25170 pts/6      0:00 ps
# /etc/crash
 dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> p
PROC TABLE SIZE = 1962
SLOT ST PID PPID PGID SID UID PRI NAME       FLAGS
  0  t   0    0    0   0   0  96 sched      load sys lock
  1  s   1    0    0   0   0  58 init       load
  2  s   2    0    0   0   0  98 pageout    load sys lock nowait
  3  s   3    0    0   0   0  60 fsflush    load sys lock nowait
 66  s 2476 719 24676 719  0  58 sh         load
 67  s 21238 21218 21218 716 20821 59 netscape load jctl
 75  s 21218 716 21218 716 20821 59 cam        load
 76  s 24529 729 24529 729  0  59 sh         load
> p -f 66
PROC TABLE SIZE = 1962
SLOT ST PID PPID PGID SID UID PRI NAME       FLAGS
 66  s 2476 719 24676 719  0  58 sh         load

             Session: sid: 719, ctty: vnode(60abe884) maj: 24 min: 6
             Process credentials: uid: 0, gid: 1, real uid: 0, real gid: 1
             as: 60022910
             wait code: 0, wait data: 0
             sig: effeb18  link 0
             parent: 600a3170       child: 60b72f80
             sibling: 0 thread: 60832840
             utime: 3             stime: 5             cutime: 24     cstime: 15
             trace: 0             sigmask: effeb10       class: 2
             lwptotal: 1         lwpcnt: 1      lwprcnt: 1
             lwpblocked: -1
```
