ongoing look at processor activity in real time. It displays a listing of the most CPU-intensive tasks on the system and can provide an interactive interface for manipulating processes. The default is to update every five seconds. The following is an example of the output from top:

```
1:36am  up 16 days,  7:50,  3 users,  load average: 1.41,  1.44,  1.21
60 processes: 58 running,  2 stopped,  0 zombie,  0 stopped
CPU states: 89.0% user,  8.5% system, 92.4% nice,  3.9% idle
Mem:  63420K av,  62892K used,   528K free, 32756K shrd,  6828K buff
Swap:  32228K av,  1096K used, 32132K free                  38052K cached
PID USER   PRI   NI  SIZE  RSS SHARE STATE  LIB  %CPU  %MEM  TIME COMMAND
```

Table 21.6 explains the values output when using the top command.

TABLE 21.6  top Fields

**Field** | **Description**
--- | ---
up | The time the system has been up and the three load averages for the system.
processes | The load averages are the average number of processes ready to run during the last 1, 5, and 15 minutes. This line is just like the output of uptime.
 | The total number of processes running at the time of the last update. This is also broken down into the number of tasks that are running, sleeping, stopped, and zombied.
CPU states | The percentage of CPU time in user mode, system mode, nice tasks, and idle. (Niced tasks are only those whose nice value is negative.) Time spent in niced tasks is also counted in system and user time, so the total is more than 100 percent.
Mem | Statistics on memory usage, including total available memory, free memory, used memory, shared memory, and memory used for buffers.
Swap | Statistics on swap space, including total swap space, available swap space, and used swap space. This and Mem are just like the output of free.
PID | The process ID of each task.
USER | The username of the task's owner.
PRI | The priority of the task.
NI | The nice value of the task. Negative nice values are lower priority.
SIZE | The size of the task's code plus data, plus stack space, in kilobytes.
RSS | The total amount of physical memory used by the task, in kilobytes.
SHARE | The amount of shared memory used by the task.
STATE | The state of the task, either S for sleeping, D for uninterruptible sleep, R for running, Z for zombied, or T for stopped or traced.