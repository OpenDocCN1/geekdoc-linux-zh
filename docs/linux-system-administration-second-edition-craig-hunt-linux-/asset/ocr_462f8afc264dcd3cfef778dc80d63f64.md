# shutdown

```
shutdown [-t sec] [options] time [warning-message]
```

The shutdown command brings down the system in a safe way. The shutdown command issues a warning to the users and to the currently running processes so that they can clean up before the system goes down. The shutdown command then sends a run level change request to the init process. If the shutdown is intended to halt the system (option -h), the requested run level is 0. If the system is to be rebooted (option -r), the run level is 6. If the shutdown is intended to put the machine in single-user mode (neither option -r nor -h), the run level is 1.

# reboot

```
reboot [options]
```

The reboot command is identical to the halt command described above, except that the system is returned to the default run level upon completion of the shutdown.

# init

```
init [run level]
```

The init command initiates a change to the specified run level. The /etc/inittab then calls the /etc/rc/rcdrc script, passing it the specified run level. The rc script causes the appropriate processes to be started for that run level. For example, to go to run level 3, the rc script runs the scripts pointed to by the symbolic links contained in the /etc/rc/rc3.d directory. The /etc/rc.d directory only exists in systems with SysV-style initialization scripts. The rc*.d directories are directly under /etc in Linux distributions that use the BSD-style initialization scripts. SuSE Linux does it a little differently still, putting the scripts that on a SysV system would be in /etc/rc.d/init.d directly in the /etc/rc.d directory. The init process will be described in some detail in Chapter 7 and was covered in Chapter 3 as well.

# kill

```
kill [-s signal] [-p] [-a] PID
kill -l [signal]
```

The kill program sends the given signal to the process whose PID is listed. By default this is the SIGTERM signal, which requests that the process terminate. Sometimes the process ignores the SIGTERM signal and has to be given a different variation of the kill command, kill -9 PID. Either the number or the signal name may be used. The number is preceded only by the hyphen, as in the kill -9 example; the signal name, however must be preceded by -s.

The kill program with the -p option does not send a signal but only outputs the PID of the process that would receive the signal if sent. To generate a list of signals, use the kill -l format, the output of which is shown below:

| 1) SIGUP | 2) SIGINT | 3) SIGQUIT | 4) SIGILL |
|---|---|---|---|
| 5) SIGTRAP | 6) SIGIOT | 7) SIGBUS | 8) SIGFPE |
| 9) SIGKILL | 10) SIGUSR1 | 11) SIGSEGV | 12) SIGUSR2 |
| 13) SIGPIPE | 14) SIGALRM | 15) SIGTERM | 17) SIGCHLD |
| 18) SIGCONT | 19) SIGSTOP | 20) SIGTSTP | 21) SIGTTIN |
| 22) SIGTTOU | 23) SIGURG | 24) SIGXCPU | 25) SIGXFSZ |
| 26) SIGVTALRM | 27) SIGPROF | 28) SIGWINCH | 29) SIGIO |
| 30) SIGPWR | | | |