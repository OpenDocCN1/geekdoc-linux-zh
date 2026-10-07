# The Solaris Multithreaded Process Architecture

links processes associated with the same terminal session. Both sessions and process groups are collections of one or more processes that have a common relation or ancestry. The two abstractions, sessions and process groups, are intimately related to each other and tied closely to the signal and terminal (tty) subsystems.

Historically, process groups and sessions arose from the desire to increase the power and flexibility available to UNIX users: developers, administrators, and end users. The process groups and sessions enable users to run multiple, concurrent jobs from a single login session, to place jobs in the background, bring them into the foreground, suspend and continue them, and toggle which job is actively connected to the control terminal (the foreground job).

The kernel maintains process groups and session links to establish an event notification chain in support of job control shells. The signal facility starts and stops processes (or jobs in this context), puts processes in the background, and brings them into the foreground. Using the process group linkage makes signal delivery to multiple, related processes much easier to implement. The sessions abstraction puts a boundary between the process group jobs and the interactive session.

Every process belongs to a process group, identified by the `pgid` pointer in the process structure, and is established in the kernel fork when the process is created. Thus, processes in the same parent/child/sibling chain, by default belong to the same process group. The process group ID (PGID) is the process ID of the process leader. That is, every process group has a process leader, where the PID and PGID are same. Sibling processes are assigned the PGID of the process; thus, the PGID of siblings is the PID of the process leader.

When a standalone process is started from a shell, it is placed in its own process group with the `setpgid(2)` system call, invoked from the shell code after the process is created with `fork(2)`. Processes grouped on a command line (e.g., a pipe) will be part of the same process group. The first process created becomes the process leader of the new process group, and subsequent processes are added to the group. Here's a quick example:

```
ksh cat report_file | sort -1 +2 | lp
```

The shell in the example is the Korn shell. Three processes will be created, one for each `cat(1)`, `sort(1)`, and `lp(1)`, and all placed in the same process group. That will be in the background, where the above `job` crunches while an interactive user session continues. In this context, a job refers to processes in the same process group working towards a common goal and connected by pipes. The proper job control keystrokes (Control-Z in `/bin/ksh`) should stop all the processes in the process group, sending a SIGSTOP to all of them. The `setpgid(2)` system call places the processes in the same group as the user's shell,