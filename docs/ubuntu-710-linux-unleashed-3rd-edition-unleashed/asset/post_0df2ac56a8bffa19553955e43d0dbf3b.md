
This example returns the owner (the user who launched the program) and the PID, along with other information, such as the percentage of CPU and memory usage, size of the command (code, data, and stack), time (or date) the command was launched, and name of the command. Processes can also be queried by PID like this:

```
```text
$ ps 6193

  PID TTY      STAT     TIME COMMAND

 6193 pts/0    S        0:00 gedit
```
```

You can use the PID to stop a running process by using the shell’s built-in kill command. This command asks the kernel to stop a running process and reclaim system memory. For example, to stop the gedit client in the example, use the kill command like this:

```
```text
$ kill 6193
```
```

After you press Enter (or perhaps press Enter again), the shell might report

```
```text
[1]+  Terminated              gedit
```
```

Note that users can kill only their own processes, but root can kill them all. Controlling any other running process requires root permission, which should be used judiciously (especially when forcing a kill by using the -9 option); by inadvertently killing the wrong process through a typo in the command, you could bring down an active system.

## Using the kill Command to Control Processes

The kill command is a basic Unix system command. You can communicate with a running process by entering a command into its interface, such as when you type into a text editor. But some processes (usually system processes rather than application processes) run without such an interface, and you need a way to communicate with them as well, so we use a system of signals. The kill system accomplishes that by sending a signal to a process, and you can use it to communicate with any process. The general format of the kill command is

```
```text
# kill option PID
```
```

A number of signal options can be sent as words or numbers, but most are of interest only to programmers. One of the most common is

```
```text
# kill PID
```
```

This tells the process with PID to stop; you supply the actual PID.

```
```text
# kill -9 PID
```
```

is the signal for kill (9 is the number of the SIGKILL signal); use this combination when the plain kill shown previously does not work.

```
# kill -SIGHUP PID
```

is the signal to “hang up”—stop—and then clean up all associated processes as well. (Its number is -1.)

As you become proficient at process control and job control, you will learn the utility of a number of kill options. A full list of signal options can be found in the signal man page.

## Using Priority Scheduling and Control

No process can make use of the system’s resources (CPU, memory, disk access, and so on) as it pleases. After all, the kernel’s primary function is to manage the system resources equitably. It does this by assigning a priority to each process so that some processes get better access to system resources and some processes might have to wait longer until their turn arrives. Priority scheduling can be an important tool in managing a system supporting critical applications or in a situation in which CPU and RAM usage must be reserved or allocated for a specific task. Two legacy applications included with Ubuntu include the nice and renice commands. (nice is part of the GNU sh-utils package, whereas renice is inherited from BSD Unix.)

The nice command is used with its -n option, along with an argument in the range of -20 to 19, in order from highest to lowest priority (the lower the number, the higher the priority). For example, to run the gkrellm client with a low priority, use the nice command like this:

```
$ nice -n 12 gkrellm &
```

The nice command is typically used for disk- or CPU-intensive tasks that might be obtrusive or cause system slowdown. The renice command can be used to reset the priority of running processes or control the priority and scheduling of all processes owned by a user. Regular users can only numerically increase process priorities (that is, make tasks less important) with this command, but the root operator can use the full nice range of scheduling (-20 to 19).

System administrators can also use the time command to get an idea of how much time and what proportion of a system’s resources are required for a task, such as a shell script. (Here, time is used to measure the duration of elapsed time; the command that deals with civil and sidereal time is the date command.) This command is used with the name of another command (or script) as an argument like this:

```
# time -p find / -name core -print
/dev/core
/proc/sys/net/core

real 61.23
```
