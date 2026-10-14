# kill PIDnumber

If you want to end all the processes you have started since login, use the kill 0 command. You do not have to know the PID numbers to use kill 0. Because this command deletes all of your processes, use this command carefully.

The following example shows how to start another find process, check its status, and then terminate it:

```
$ find / -type f -print > dir.paths &
38
$ ps
PID TT STAT TIME COMMAND
520 p4 I 0:11:10 sh
38 p5 I 0:10:33 find
1216 p6 S 0:01:14 qdaemon
839 p7 R 0:03:55 ps
$ kill 38
$ ps
38 Terminated
PID TT STAT TIME COMMAND
520 p4 I 0:11:35 sh
1216 p6 S 0:01:11 qdaemon
839 p7 R 0:03:27 ps
$
```

The command kill 38 stops the background find process, and the second ps command returns no status information about PID number 38. The system does not display the termination message until you enter your next command.

In the previous example, kill 38 and kill 0 have the same effect because only one process was started from this terminal or workstation.

In the C shell, the kill command has the following format:

# kill % jobnumber

The following example uses the C shell to start another find process, to check its status with the jobs command, and then to terminate it:

```
% find / -type f -print > dir.paths &
[3] 40
% jobs -l
[3] +40 Running find / -type f -print > dir.paths &
% kill %3
% jobs -l
[3] +Terminated find / -type f -print > dir.paths
%
```