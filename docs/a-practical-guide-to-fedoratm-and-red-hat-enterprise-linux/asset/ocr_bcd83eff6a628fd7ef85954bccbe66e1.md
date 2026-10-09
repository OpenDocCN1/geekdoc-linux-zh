that the shell is still being run by the same process but that it forked another process to run `sleep`:

```
$ sleep 10 &
[1] 22791
$ ps -f
```

UID PID PPID C STIME TTY TIME CMD
max 21341 21340 0 10:42 pts/16 00:00:00 bash
max 22791 21341 0 17:31 pts/16 00:00:00 sleep 10
max 22792 21341 0 17:31 pts/16 00:00:00 ps -f

You can also use `pstree` (or `ps --forest`, with or without the `–c` option) to see the parent-child relationship of processes. The next example shows the `–p` option to `pstree`, which causes it to display PID numbers:

```
$ pstree -p
systemd(1)───NetworkManager(655)───{NetworkManager}(702)
|    ├─abrtwd(657)───abrt-dump-oops(696)
|    ├─accounts-daemon(1204)───{accounts-daemo}(1206)
|    └─agetty(979)
...
|    ├─login(984)───bash(2071)───pstree(2095)
|    '        '─sleep(2094)
...
```

The preceding output is abbreviated. The first line shows the PID 1 (`systemd` `init`) and a few of the processes it is running. The line that starts with `–login` shows a textual user running `sleep` in the background and `pstree` in the foreground. The tree for a user running a GUI is much more complex. Refer to “$%: PID Number” on page 1028 for a description of how to instruct the shell to report on PID numbers.

# ## EXECUTING A COMMAND

`fork()` and `sleep()`  When you give the shell a command, it usually forks [spawns using the `fork()` system call] a child process to execute the command. While the child process is executing the command, the parent process [running the shell] `sleeps` [implemented as the `sleep()` system call]. While a process is sleeping, it does not use any computer time; it remains inactive, waiting to wake up. When the child process finishes executing the command, it tells its parent of its success or failure via its exit status and then dies. The parent process (which is running the shell) wakes up and prompts for another command.

`Background process`  When you run a process in the background by ending a command with the ampersand control operator (`&`), the shell forks a child process without going to sleep and without waiting for the child process to run to completion. The parent process, which is executing the shell, reports the job number and PID number of the child process and prompts for another command. The child process runs in the background, independent of its parent.

`Builtins`  Although the shell forks a process to run most commands, some commands are built into the shell (e.g., `cd`, `alias`, `jobs`, `pwd`). The shell does not fork a process to run builtins. For more information refer to “Builtins” on page 170.