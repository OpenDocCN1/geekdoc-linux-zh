# ps 1135

```
103 ? 0:00 in.route
140 ? 0:00 inetd
115 ? 0:00 keyserv
162 ? 0:00 automoun
145 ? 0:00 statd
147 ? 0:00 lockd
305 ? 0:00 listen
166 ? 0:01 syslog
180 ? 0:00 cron
196 ? 0:00 lpsched
217 ? 0:00 sendmail
205 ? 0:02 lp
307 ? 0:14 Xsun
214 ? 0:00 powered
...(More information not shown)
```

The columns are described:

| PID | Process identification number. |
| TTY | The terminal which the process (or its parent) started. If the process has no controlling terminal, this column contains a question mark ( Processes with question marks are usually system processes. |
| TIME | The cumulative amount of CPU time used by the process. |
| CMD | The name of the command that generated the process. Note, that for ps -el command, the first eight characters of the file name are displayed. |

When you type ps -el and press Return, you get a list that looks like the following

| F | UID | PID | PPID | C PRI NI | ADDR | SZ | WCHAN TTY | TIME CMD |
| 19 T | 0 | 0 | 0 | 0 SY | f0274e38 | ? | 0:01 sched |
| 18 S | 1 | 0 | 0 | 41 20 | f02bda288 | 4 f02bda86 | 0:00 init |
| 19 S | 0 | 2 | 0 | 0 SY | f52b2d1c | ? f0286a4? | 0:00 pageout |
| 19 S | 0 | 3 | 1 | 0 SY | f52b2c08 | 350 f5a8be4 | 0:21 flashlu |
| 186 S | 0 | 242 | 1 | 59 20 | f52bd2ff | 511 f5a83d7e | 0:01 void |
| 305 S | 0 | 302 | 1 | 41 20 | f52bd2b8 | 480 f5a8cd4 | 0:00 cmd |
| 118 S | 0 | 113 | 1 | 45 20 | f52bd8f36 | f5a81c7 | 0:00 sac |
| 103 S | 0 | 103 | 1 | 41 20 | f52bd2d9 | 340 f5a8df86 | 0:00 rpcbind |
| 140 S | 0 | 140 | 1 | 54 20 | f52d1d20 | 446 f5a3e6 | 0:00 in.route |
| 115 S | 0 | 115 | 1 | 57 20 | f52bd3c10 | 461 f5a8bbe2 | 0:00 keyserv |
| 162 S | 0 | 162 | 1 | 41 20 | f52dc4c50 | 560 3e19c? | 0:00 automoun |
| 145 S | 0 | 145 | 1 | 65 20 | f52bd2b0 | 501 f5a89f6 | 0:00 staat |
| 147 S | 0 | 147 | 1 | 65 20 | f52bd2b0 | 409 f5a83df8 | 0:00 lockd |
| 305 S | 0 | 305 | 2 | 41 20 | f52bd5f20 | 702 f5a8cd36 | 0:00 listen |
| 196 S | 0 | 196 | 1 | 46 20 | f52e1859 | 489 f5a8118 | 0:01 syslog |
| 180 S | 0 | 180 | 1 | 51 20 | f52e1b18 | 358 f5a8be8 | 0:00 cron |
| 217 S | 0 | 217 | 1 | 41 20 | f75e1458 | 448 f5a83da0 | 0:00 lached |
| 205 S | 0 | 205 | 1 | 41 20 | f52e169d | 462 f16f90 | 0:02 lp |
| 1001 S | 0 | 307 | 2 | 41 20 | f52e166d8 | 343 f5a83586 | 0:17 Xsun |
| 214 S | 0 | 214 | 1 | 58 20 | f52e1610 | 215 f5216210 | 0:00 powered |