# Monitoring and Managing Linux PROCESSES

```
[user@host-$] kill 5194
[user@host-$] ps aux | grep job
user      5199 0.0 0.222448 312 pts/1 S    16:39 0:00 /bin/bash /home/
user/control job2
user      5205 0.0 0.222448 314 pts/1 S    16:39 0:00 /bin/bash /home/
user/control job3
user      5783 0.0 0.221860 964 pts/1 S+   16:43 0:00 grep --color=auto
job
[1] Terminated
[user@host-$] kill 5199
[user@host-$] ps aux | grep job
user      5205 0.0 0.222448 314 pts/1 S    16:39 0:00 /bin/bash /home/
user/control job3
user      5938 0.0 0.221860 1048 pts/1 S+   16:44 0:00 grep --color=auto
job
[2]- Killed control job2
[user@host-$] kill -SIGTERM 5205
user      5996 0.0 0.221860 1048 pts/1 S+   16:45 0:00 grep --color=auto
job
[3]+ Terminated control job3
```

The kill command can signal multiple processes, based on their command name.

```
[user@host-$] ps aux | grep job
5194 0.0 0.222448 2980 pts/1 S    16:39 0:00 /bin/bash /home/user/
control job1
5199 0.0 0.222448 3132 pts/1 S    16:39 0:00 /bin/bash /home/user/
control job2
5205 0.0 0.222448 3124 pts/1 S    16:39 0:00 /bin/bash /home/user/
control job3
5438 0.0 0.221860 1096 pts/1 S+   16:41 0:00 grep --color=auto job
[user@host-$] kill control
[1] Terminated control job1
[2]- Terminated control job2
[3]+ Terminated control job3
[user@host-$]
```

Use kill to send a signal to one or more processes selection criteria can be a command name, processes owned by a specific user, or system-wide processes. The kill command includes advanced selection criteria:

+   - Command - Processes with a pattern-matched command name.
- UID - Processes owned by a Linux user account, effective or real.
- GID - Processes owned by a Linux group account, effective or real.
- Parent - Processes of a specific parent process.
- Terminal - Processes running on a specific controlling terminal.

```
[user@host-$] ps aux | grep job
user      5992 0.0 0.222448 3040 pts/1 S    16:59 0:00 /bin/bash /home/
user/bin/control kill1
user      5996 0.0 0.222448 3048 pts/1 S    16:59 0:00 /bin/bash /home/
user/bin/control kill2
user      6884 0.0 0.222448 3048 pts/1 S    16:59 0:00 /bin/bash /home/
user/bin/control kill3
```