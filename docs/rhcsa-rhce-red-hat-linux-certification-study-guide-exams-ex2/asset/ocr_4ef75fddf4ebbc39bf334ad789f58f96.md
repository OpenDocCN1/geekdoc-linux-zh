# FIGURE 9-5

Output from the ps aux command

```
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.0 0.0 19244 1340 ? Ss Jan19 0:05 /sbin/init
root 2 0.0 0.0 0 0 ? S Jan19 0:00 [kthreadd]
root 3 0.0 0.0 0 0 ? S Jan19 0:00 [migration/0]
root 4 0.0 0.0 0 0 ? S Jan19 0:00 [ksoftirqd/0]
root 5 0.0 0.0 0 0 ? S Jan19 0:00 [watchdog/0]
root 6 0.0 0.0 0 0 ? S Jan19 0:00 [migration/1]
root 7 0.0 0.0 0 0 ? S Jan19 0:01 [ksoftirqd/1]
root 8 0.0 0.0 0 0 ? S Jan19 0:00 [watchdog/1]
root 9 0.0 0.0 0 0 ? S Jan19 0:00 [migration/2]
root 10 0.0 0.0 0 0 ? S Jan19 0:05 [ksoftirqd/2]
root 11 0.0 0.0 0 0 ? S Jan19 0:00 [watchdog/2]
root 12 0.0 0.0 0 0 ? S Jan19 0:00 [migration/3]
root 13 0.0 0.0 0 0 ? S Jan19 0:01 [ksoftirqd/3]
root 14 0.0 0.0 0 0 ? S Jan19 0:00 [watchdog/3]
root 15 0.0 0.0 0 0 ? S Jan19 0:01 [events/0]
root 16 0.0 0.0 0 0 ? S Jan19 0:24 [events/1]
root 17 0.0 0.0 0 0 ? S Jan19 0:12 [events/2]
root 18 0.0 0.0 0 0 ? S Jan19 0:04 [events/3]
root 19 0.0 0.0 0 0 ? S Jan19 0:00 [khelper]
root 20 0.0 0.0 0 0 ? S Jan19 0:00 [khelper]
root 21 0.0 0.0 0 0 ? S Jan19 0:00 [netns]
root 22 0.0 0.0 0 0 ? S Jan19 0:00 [async/mgr]
```

# TABLE 9-1

Columns of Output from ps aux

| Column Title | Description |
|---|---|
| USER | The username associated with the process |
| PID | Process Identifier |
| %CPU | Current CPU usage |
| %MEM | Current RAM usage |
| VSZ | Virtual memory size of the process in KB |
| RSS | Physical memory in use by the process, not including swap space, in KB |
| TTY | Associated terminal console |
| STAT | Process status |
| START | Start time of the process; if you just see a date, the process started more than 24 hours ago |
| TIME | Cumulative CPU time used |
| COMMAND | Command associated with the process |