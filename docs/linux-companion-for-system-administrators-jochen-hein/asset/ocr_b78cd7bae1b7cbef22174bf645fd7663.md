# Process tree

For each process, the kernel stores the ID of the process that generated it. This is also called the parent process. The newly started processes are child processes. By means of the `pstree command, which does not exist under other UNIX systems, you can gain an overview of the hierarchy in the process table.

# Process management

A program that has a controlling terminal can usually be aborted with Ctrl-(the interrupt character, also see stty -a). Many processes (for example network daemons) under UNIX have no associated terminal and cannot be controlled with key combinations. It is obviously necessary to address these processes as well; this is one of the applications of the concept of signals. And how a program reacts to signals is implementation-dependent and is usually documented in the man page. The default reaction to many signals is the termination of the program.

The kill program is not only used to abort programs, but also simply to send signals. Signals can be specified either numerically or symbolically. Table 10.8 shows the most important signals; all signals can be listed by means of kill -1.

The signal 0 has a special meaning: the kernel checks that the process exists but does not send a signal. This can be used to check whether or not a task is running. The example in Listing 10.67 checks if a process setiatome is running, and starts it if it is not running.

```
$ crontab -l | killall 0 setiatome | setiatome
```

**Listing 10.67** Using killall to ensure a program is running.

| Signal | Number | Meaning |
| --- | --- | --- |
| SIGHUP | 1 | Hang-up, re-read configuration |
| SIGKILL | 9 | Unconditional program termination |
| SIGUSR1 | 10 | User-defined signal |
| SIGUSR2 | 12 | User-defined signal |
| SIGTERM | 15 | Normal program termination |

**Table 10.8** The most important signals.

It is often necessary to send a daemon a hang-up signal (SIGHUP); this causes many daemons to re-read their configuration file. You can find out the