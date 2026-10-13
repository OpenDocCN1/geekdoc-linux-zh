| Argument | Description |
|---|---|
| **-s key** | Sorts the report in descending order based on key (cpu, time, size, rss, or pri). |
| **-S key** | Sorts the report in ascending order based on key (cpu, time, size, rss, or pri). |
| **-t** | Reports a total usage summary for each user. |
| **-u euids** | Reports only processes whose effective UID is listed in *euids*. |
| **-U uids** | Reports only processes whose real UID is listed in *uids*. |
| **-v** | Reports using verbose mode, which includes the percentage of time in user mode and system mode. |

The following example uses the **prstat** command to list the processes associated with the dla user account:

```
```text
$ prstat -c -u dla
PID USER  SIZE RSS STATE PRI NICE TIME       CPU PROCESS/NLWP
9830 dla   812K 696K cpu0  48  0    0:00:00.0 2%  prstat/1
9789 dla   2960K 2136K sleep 59 0    0:00:00.0 1%  xterm/1
9790 dla   808K 628K sleep 48 0    0:00:00.0 0%  sh/1
Total: 3 processes, 3 lwps, 1 load averages: 0.00, 0.00, 0.01
$
```
```

![](bbox=[0.148, 0.53, 0.252, 0.598])

Be sure you understand that both **ps** and **prstat** provide information about active processes. The **ps** command provides more user-oriented information (parent PID, TTY, start date, and so on), whereas the **prstat** command provides more system-oriented information (process size, priority, CPU utilization, and so on).

# The kill Command

The kill(1) command terminates a process by sending a signal to it that causes it to exit. Many different types of signals exist. The signals typically used to terminate a process are listed in Table 7.3, and a complete listing of base signals can be found in signal(3HEAD).

The default response of processes that receive these signals is to terminate, but this behavior can be changed on a process-by-process basis.

| Symbolic Name | Value | Description |
|---|---:|---|
| SIGHUP | 1 | Hangup |
| SIGINT | 2 | Interrupt |