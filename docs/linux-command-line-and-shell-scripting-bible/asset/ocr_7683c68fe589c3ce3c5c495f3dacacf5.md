# the renice command

Sometimes you'd like to change the priority of a command that's already running on the system. That's what the renice command is for. It allows you to specify the PID of a running process to change the priority of:

```
$ ./test4 > test4 &\n[1] 29504
$ ps al
F UID PID PPID NI WCHAN STAT TTY TIME COMMAND
100 501 29459 29458 12 wait4 S pts/0 0:00 -bash
000 501 29504 29459 9 wait4 S pts/0 0:00 /bin/bash
000 501 29518 29504 9 nanolol S pts/0 0:00 sleep 10
000 501 29519 29549 14 0 - R pts/0 0:00 al
$ renice -10 old priority, new priority 10
29504: old priority 0
$ ps al
F UID PID PPID NI WCHAN STAT TTY TIME COMMAND
100 501 29459 29458 16 wait4 S pts/0 0:00 -bash
000 501 29504 29459 10 wait4 SN pts/0 0:00 /bin/bash
000 501 29535 29504 9 nanolol S pts/0 0:00 sleep 10
000 501 29537 29504 14 0 - R pts/0 0:00 al
```

The renice command automatically updates the scheduling priority of the running process. Just as with the nice command, the renice command has some limitations:

+   - You can only renice processes that you own.
- You can only renice your processes to a lower priority.
- The root user can renice any process to any priority.

If you want to fully control processes, you must be logged in as your account.

# Running Clockwork

I'm sure that, as you start working with scripts, there'll be a situation in which you'll want to run a script at a preset time, usually at a time when you're not. The Linux system provides ways of running a script at a preselected time:

+   - The at command
- The batch command
- The cron table

Each method uses a different technique for scheduling when and how to run ps al. The following sections describe each of these methods.