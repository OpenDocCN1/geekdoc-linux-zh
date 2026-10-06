# Managing Processes

15 (SIGTERM). You can also use the shortened form -signal. If you do this and a signal name, you should use the SIG PID option of the name—for instance, use KILL rather than SIGKILL. The pid option is, of course, the PID for the process you want to kill. Obtain this number from ps or top.

The kill program will kill those processes owned by the user who runs kill. The exception is if that user is root; the superuser may kill any user's processes.

![](bbox=[0.142, 0.206, 0.237, 0.253])

# Real World Scenario

# Running Programs Persistently

Signals can be passed to the kernel even if you don't use the kill command. For instance, when you log out of a session, the programs you started from that session are sent the SIGHUP signal, which causes them to terminate. If you want to run a program that will continue running even when you log out, you can launch it with the `nohup` program:

```
$ nohup program options
```

This command causes the program to ignore the SIGHUP signal. It can be handy if you want to launch small servers that may legitimately be run as ordinary users.

A variant on kill is killall, which has the following form:

```
killall [options] [-- name [...]
```

This command kills a process based on its name rather than its PID number. For instance, `kill vi` kills all the running processes vi. You may specify the short form (-signal?) by preceding the signal with -s or --signal. With kill, the default is 15 (SIGTERM). One potentially important option to killall is -i, which causes kill to ask for confirmation before sending the signal to each process. You might use it like this:

```
$ kill -i vi
```

```
kill vi (13211) ? (y/n) y
kill vi (13217) ? (y/n) n
```

In this example, two instances of the Vi editor were running, but only one should have been killed. As a general rule, if you run kill as root, you should use the -i parameter. If you don't, it's all too likely that you'll kill processes that you shouldn't, particularly causes the computer is being used by many people at once.