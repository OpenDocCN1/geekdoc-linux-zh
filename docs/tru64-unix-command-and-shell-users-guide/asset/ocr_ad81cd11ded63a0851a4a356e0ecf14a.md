# ps

In Example 6-1, the ps command displays the status of all processes associated with your workstation.

# Example 6-1: Output from the ps Command

```
$ ps
PID TTY STAT TIME CMD
29670 p4 I 0:00.00 -csh (csh)
515 p5 S 0:00.00 -csh (csh)
28476 p5 R 0:00.00 ps
790 p6 I 0:00.00 -csh (csh)
$
```

You interpret the display under these entry headings as follows:

PID
Process identification. The system assigns a process identification number (PID number) to each process when that process starts. There is no relationship between a process and a particular PID number; that is, if you start the same process several times, it will have a different PID number each time.

TTY
Controlling terminal device name. On a system with more than one workstation, this field tells you which workstation started the process. On a system with only one workstation, this field can contain the designation console or the designation for one or more virtual terminals.

STAT
Symbolic process status. The system displays the state of the process, with a sequence of up to four alphanumeric characters. For more information, see the ps(1) reference page.

TIME
Time devoted to this process by the computer is displayed in minutes, seconds, and hundredths of seconds starting when you enter ps.

CMD
The name of the command (or program) that started the process.

You can also check the status of a particular process by using the -p flag and the PID number with the ps command. The general format for checking the status of a particular process is the following:

```
ps -p PIDnumber
```

The ps command also displays the status of background processes. If there are any background processes running, they will be displayed along with the foreground processes. The following example shows how to start a find background process and then check its status:

```
$ find / -type f -print > dir.paths &
25
$ ps -p25
PID TTY TIME CMD
25 console 0:40.00 find
$
```