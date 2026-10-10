the process has been stopped:

```
$ sleep 60
^Z
[1] + Stopped sleep 60
$
```

The number in the square brackets is the job number assigned by the shell. The shell refers to each process running in the shell as a job and assigns each job a unique number within the current shell. It assigns the first started process job number 1, the second job number 2, and so on.

If you have a stopped job assigned to your shell session, Bash warns you the first time you try to exit the shell:

```
$ sleep 70
^Z
[2] + Stopped sleep 70
$
$ exit
logout
There are stopped jobs.
$
```

You can view the stopped jobs using the ps command:

```
$ ps -l
F S UID PID PPID [ ... ] TTY TIME CMD
F S 1001 1509 1508 [ ... ] pts/0 00:00:00 bash
0 T 1001 1532 1509 [ ... ] pts/0 00:00:00 sleep
0 T 1001 1533 1509 [ ... ] pts/0 00:00:00 sleep
0 R 1001 1534 1509 [ ... ] pts/0 00:00:00 ps
$
```

In the s column (process state), the ps command shows the stopped job's state as T. This indicates the command is either being traced or is stopped.

If you really want to exit the shell with a stopped job (or jobs) still active, just type the exit command again. The shell exits, terminating the stopped job.

Alternately, now that you know the PID of the stopped job(s), you can use the kill command to send a SIGKILL (9) signal to terminate it: