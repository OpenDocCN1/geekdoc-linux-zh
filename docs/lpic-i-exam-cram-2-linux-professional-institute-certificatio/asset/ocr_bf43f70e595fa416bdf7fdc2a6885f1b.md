If you type the `kill` command and the process ID (PID) of a program, the `15` or `SIGTERM` signal is sent to that program.

`SIGHUP = 1`

The `SIGHUP`, `HUP`, or `1` signal is a special case. It’s what we could call a *bounce* signal, where the process isn’t just killed but instead is signaled to end itself and then restart itself. The most frequently used reason for doing this is to have a process such as a server daemon stop, reread its configuration files, and then start back up.

`SIGKILL = 9`

The `SIGKILL` or `9` signal is the ultimate kill signal. Even if a process is a zom-bie (can’t be killed by any other means), a `kill -9` `PID` command usually kills the process and removes it from memory. The process being `SIGKILL`ed has no opportunity to save data or do anything else.

Here are a couple of examples of usage:

```
```
kill PID (Politely kills the process, allows saves)
kill -9 PID or kill -KILL PID (puts a bullet in the process, no saves)
kill -1 PID or kill -HUP PID (bounces or restarts processes)
```
```

# # Managing Process Priorities

Linux uses a combination of priority and scheduling to run multiple process-es in what appears to be multitasking on a single processor. On multiple processors, this makes for actual multitasking.

Strangely enough, the process priorities are backward like a lot of other things, and they stretch from the highest (`20`) to the lowest (`19`) (see Figure 2.1).

![](bbox=[0.1, 0.72, 0.8, 0.8])

**Figure 2.1**    Linux process priorities.

A process’s default priority is normally `0` when started, unless the program-mer has a need to set the starting priority higher. Although users can lower (from `0` to `19`) a process’s priority, only the root user can take a process to a higher (`0` to `-20`) priority.