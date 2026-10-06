# Process

Process is the name given to the situation where the file is working. When you run a program, it will be loaded into memory to process the program name. Except the processes that we start in our system, there are many services and processes are running in the system. Running programs at the same time may consist of multiple processes.

# Ps

We use ps command to view any currently running processes. To learn use a parameter of this command we can use ps --help (a=all) command. I used the command aux and the screen output.

```
root@local:~$ ps aux
USER       PID CPU MEM VSZ RSS TTY START TIME COMMAND
root      1 0.1 0.6 24184 0 ? S 23:36 0:00 [/bin/init]
root      7 0.0 0.0 0 ? S 23:36 0:00 [thread]
root      3 0.0 0.0 0 ? S 23:36 0:00 [kthread/0]
root      5 0.0 0.0 0 ? S 23:36 0:00 [kworker/0-eventshi]
root      7 0.0 0.0 0 ? S 23:36 0:00 [rcu_sched]
root      8 0.0 0.0 0 ? S 23:36 0:00 [rcu_bh]
root      9 0.0 0.0 0 ? S 23:36 0:00 [migration/0]
root     10 0.0 0.0 0 ? S 23:36 0:00 [watchdog/0]
root     11 0.0 0.0 0 ? S 23:36 0:00 [khelper]
```

Of course which parameter works for the best, using our comamnd with those parameters would be a better idea. We can use some commands as these:

+   - ps: Processes relating to the active user.
- ps -e: All processes running the running
- ps -e or ps -f: For a detailed list of the processes running in the system.
- ps -u <user>: Processes relating to a user in the system