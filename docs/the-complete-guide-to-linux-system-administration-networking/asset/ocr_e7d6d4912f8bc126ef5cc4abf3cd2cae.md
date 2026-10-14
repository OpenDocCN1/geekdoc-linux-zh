![](bbox=[0.2, 0.13, 0.7, 0.64])

# Figure 6-5 The GNOME System Monitor utility Resource Monitor tab

based on the programs they are running. A very fast CPU can tolerate a high load level and still deliver acceptable response times.

When you decide to investigate the cause of a high load, begin by using top or one of the graphical utilities to see if a single process is using a high percentage of CPU time. A "runaway process" started by a user might be the cause of the heavy load. In this case, you can change the priority of the process, talk to the user who started the process, and kill the process if necessary. As you become more familiar with the normal load on your system, you will be able to tell from a small load graphic on your Panel when a single process has suddenly run wild (for example, because of incoming network traffic or a programming bug).

When many legitimate processes are causing the heavy CPU load, the ps and top command options (or the graphical utilities) can help you determine whether one set of programs (such as the Web server), one type of program (such as shell scripts), or one user's programs are causing the heavy load. In each case, when you know the details, you can take corrective action by renicing a set of processes based on the command name or the user name.