# RHEL 9 System and Process Monitoring

```
# ps -u john
  PID TTY      TIME CMD
  914 ?        00:00:00 systemd
  915 ?        00:00:00 (sd-pam)
  970 ?        00:00:00 gnome-keyring-d
  974 tty1      00:00:00 gdm-x-session
  .
  .
```

Note that each process is assigned a unique process ID which can be used to stop the process by sending it a termination (TERM) signal via the kill command. For example:

```
$ kill 13217
```

The advantage of ending a process with the TERM signal is that it allows the process to exit gracefully, potentially saving any data that might otherwise be lost.

If the standard termination signal does not terminate the process, repeat the kill command with the -9 option. This command sends a KILL signal which should cause even frozen processes to exit but does not give the process a chance to exit gracefully, possibly resulting in data loss:

```
$ kill -9 13217
```

To list all of the processes running on a system (including all user and system processes), execute the following command:

```
$ ps -ax
  PID TTY      STAT  TIME COMMAND
   1 ?        Ss     0:22 /usr/lib/systemd/systemd rhgb --switched-root
   2 ?        S      0:00 [kthreadd]
   3 ?        I<     0:00 [rcu_gp]
   4 ?        I<     0:00 [rcu_par_gp]
   5 ?        I<     0:00 [netns]
```

To list all processes and include information about process ownership, CPU, and memory use, execute the ps command with the -aux option:

```
$ ps -aux
USER       PID %CPU %MEM   VSZ   RSS TTY      STAT START   TIME COMMAND
root         2  0.0  0.0     0     0 ?        S    09:59   0:00 [kthreadd]
root         3  0.0  0.0     0     0 ?        I<   09:59   0:00 [rcu_gp]
root         4  0.0  0.0     0     0 ?        I<   09:59   0:00 [rcu_par_gp]
root         5  0.0  0.0     0     0 ?        I<   09:59   0:00 [netns]
root         7  0.0  0.0     0     0 ?        I<   09:59   0:00 [kworker/0:0H-
events_highpri]
root         9  0.0  0.0     0     0 ?        I<   09:59   0:00 [kworker/0:1H-
events_highpri]
.
.
demo      9788  0.1  1.4 763248 50480 ?        Ssl   15:05   0:00 /usr/libexec/
```