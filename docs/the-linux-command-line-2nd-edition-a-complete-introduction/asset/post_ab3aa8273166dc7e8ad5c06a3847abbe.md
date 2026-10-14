
The kernel maintains information about each process to help keep things organized. For example, each process is assigned a number called a process ID or PID. PIDs are assigned in ascending order, with init always getting PID 1. The kernel also keeps track of the memory assigned to each process, as well as the processes’ readiness to resume execution. Like files, processes also have owners and user IDs, effective user IDs, etc.

## Viewing Processes

The most commonly used command to view processes (there are several) is ps. The ps program has a lot of options, but in it simplest form it is used like this:

```
[me@linuxbox ~]$ ps
PID TTY          TIME CMD
 5198 pts/1    00:00:00 bash
10129 pts/1    00:00:00 ps
```

The result in this example lists two processes, process 5198 and process 10129, which are bash and ps respectively. As we can see, by default, ps doesn’t show us very much, just the processes associated with the current terminal session. To see more, we need to add some options, but before we do that, let’s look at the other fields produced by ps. TTY is short for "Teletype," and refers to the controlling terminal for the process. Unix is showing its age here. The TIME field is the amount of CPU time consumed by the process. As we can see, neither process makes the computer work very hard.

If we add an option, we can get a bigger picture of what the system is doing:

```
[me@linuxbox ~]$ ps x
PID TTY      STAT   TIME COMMAND
 2799 ?        Ssl    0:00 /usr/libexec/bonobo-activation-server -ac
 2820 ?        Sl     0:01 /usr/libexec/evolution-data-server-1.10 --
15647 ?        Ss     0:00 /bin/sh /usr/bin/startkde
15751 ?        Ss     0:00 /usr/bin/ssh-agent /usr/bin/dbus-launch --
15754 ?        S      0:00 /usr/bin/dbus-launch --exit-with-session
15755 ?        Ss     0:01 /bin/dbus-daemon --fork --print-pid 4 -pr
15774 ?        Ss     0:02 /usr/bin/gpg-agent -s -daemon
15793 ?        S      0:00 start_kdeinit --new-startup +kcminit_start
15794 ?        Ss     0:00 kdeinit Running...
15797 ?        S      0:00 dcopserver -nosid

and many more...
```

Adding the “x” option (note that there is no leading dash) tells ps to show all of our processes regardless of what terminal (if any) they are controlled by. The presence of a “?” in the TTY column indicates no controlling terminal. Using this option, we see a list of every process that we own.

Since the system is running a lot of processes, ps produces a long list. It is often helpful to pipe the output from ps into less for easier viewing. Some option combinations also produce long lines of output, so maximizing the terminal emulator window may be a good idea, too.

A new column titled STAT has been added to the output. STAT is short for “state” and reveals the current status of the process:

## Table 10-1: Process States

| State | Meaning |
|-------|---------|
| R | Running. This means that the process is running or ready to run. |
| S | Sleeping. The process is not running; rather, it is waiting for an event, such as a keystroke or network packet. |
| D | Uninterruptible Sleep. Process is waiting for I/O such as a disk drive. |
| T | Stopped. Process has been instructed to stop. More on this later. |
| Z | A defunct or “zombie” process. This is a child process that has terminated, but has not been cleaned up by its parent. |
| < | A high priority process. It’s possible to grant more importance to a process, giving it more time on the CPU. This property of a process is called niceness. A process with high priority is said to be less nice because it’s taking more of the CPU’s time, which leaves less for everybody else. |
| N | A low priority process. A process with low priority (a “nice” process) will only get processor time after other processes with higher priority have been serviced. |

The process state may be followed by other characters. These indicate various exotic process characteristics. See the ps man page for more detail.

Another popular set of options is “aux” (without a leading dash). This gives us even more information:
