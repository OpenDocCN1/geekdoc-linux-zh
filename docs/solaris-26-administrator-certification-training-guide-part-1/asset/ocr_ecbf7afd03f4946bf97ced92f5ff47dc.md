As system administrator, you can use the renice command to change the priority of a process after it has been submitted. The renice command has the following form:

```
renice priority -n <value> -p <pid>
```

Use the ps -el command to find the PID of the process for which you want to change the priority. The process you want to change in the following example is named "largejob":

```
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
9 S 0 8200 4100 0 84 20 f0274e38 193 ? 0:00 largejob
```

Issue the following command to increase the priority of PID 8200:

```
renice -n -4 -p 8200
```

Issuing the ps -el command again shows the process with a higher priority:

```
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
9 S 0 8200 4100 0 60 12 f0274e38 193 ? 0:00 largejob
```

# Changing the Scheduling Priority of Processes with priocntl

The standard priority scheme has been improved under Solaris as part of its support for real-time processes. Real-time processes are designed to work in applications areas in which nearly immediate response to events is required. These processes are given nearly complete access to all system resources when they are running. Solaris uses time-sharing priority numbers ranging from -20 to 20. Solaris uses the priocntl command, intended as an improvement over the nice command, to modify process priorities. To use priocntl to change a priority on a process, type

```
priocntl -s -p <new-priority> -i pid <process-id>
```

where new-priority is the new priority for the process and process-id is the PID of the process you wish to change. The following example sets the priority level for process 8200 to -5:

```
priocntl -s -p -5 -i pid 8200
```

The following example is used to set the priority (nice value) for every process created by a given parent process:

```
priocntl -s -p -5 -I ppid 8200
```

As a result of this command, all processes forked from process 8200 will have a priority of -5.

Consult the online manual pages for more information about the priocntl command.