# # Killing a Process

If you issue the ps command and find that one of your processes is hung, or if you started a large job that you wish to stop, you can do so with the kill command. kill is a utility that sends a signal to the process you identify. You can kill any process that you own. In addition, the superuser can kill almost any process on the system.

To kill a process that you own, simply issue the kill command and the Process ID (PID). The following example shows issuing the ps command to find all processes owned by martyp, killing a process, and checking to see that it has disappeared:

```
```
martyp $ ps -ef | grep martyp
martyp    19336    19334  0   05:24:32 pts/4      0:01 -ksh
martyp    19426    19336  0   06:01:01 pts/4      0:00 grep martyp
martypl   19424    19336  5   06:00:48 pts/4      0:01 find /-name .login
martypl $ kill 19424
martypl $ ps -ef | grep martyp
martypl   19336    19334  0   05:24:32 pts/4      0:01 -ksh
martypl   19428    19336  1   06:01:17 pts/4      0:00 grep martyp
[1]+    Terminated      find / -name .login &
martypl $```
```

The example shows killing process 19424, which is owned by martyp. We confirm that the process has indeed been killed by reissuing the ps command. You can also use the -u option to ps to list processes with the login name you specify.

You can kill several processes on the command line by issuing kill followed by a space-separated list of all the process numbers you wish to kill.

Take special care when killing processes if you are logged in as superuser. You may adversely affect the way the system runs and have to manually restart processes or reboot the system.

# ## Signals

When you issue the kill command and process number, you are also sending a signal associated with the kill. We did not specify a signal in our kill