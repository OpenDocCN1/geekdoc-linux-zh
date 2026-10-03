In addition, the CDE Process Manager, which was described earlier, can be used to kill processes. In the Process Manager window, highlight the process that you want to terminate, click Process from the toolbar at the top of the window, and then select Kill from the pull-down menu as shown in Figure 9.6.

![](bbox=[0.048, 0.217, 0.593, 0.425])

FIGURE 9.6
Killing processes

The equivalent UNIX command used by the Process Manager to terminate a process is

```
kill -9 <PID>
```

where <PID> is the process ID of the selected process.

# SCHEDULING PROCESSES

Processes compete for execution time. Scheduling, one of the key elements in a time-sharing system, determines which of the processes will execute next. Although hundreds of processes might be present on the system, only one actually uses the CPU at any given time. Time-sharing on a CPU involves suspending a process and then restarting it later. Because the suspension and resumption of active processes occurs several times each second, it appears to the user that the system is performing many tasks simultaneously.

UNIX attempts to manage the priorities of processes by giving a higher priority to those that have used the least amount of the CPU. In addition, processes that are sleeping on an event, such as a keyboard press, get higher priority than processes that are purely CPU-driven.

> NOTE
You can redefine the command performed by the Kill menu item to a different command by redefining the action labeled “Kill” in the file:

/usr/dt/appconfig/types/C/sdtprocess.dt

See Appendix B “Administration and Configuration of the CDE” for details on configuring CDE.