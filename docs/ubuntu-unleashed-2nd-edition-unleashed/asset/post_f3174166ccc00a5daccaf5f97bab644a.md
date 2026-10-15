
This example returns the owner (the user who launched the program) and the PID, along with other information, such as the percentage of CPU and memory usage, size of the command (code, data, and stack), time (or date) the command was launched, and the name of the command. Processes can also be queried by PID like this:

```text
$ ps 5918
  PID TTY      STAT   TIME COMMAND
 5918 pts/0    S      0:00 xosview
```

You can use the PID to stop a running process by using the shell’s built-in kill command. This command asks the kernel to stop a running process and reclaim system memory. For example, to stop the xosview client in the example, use the kill command like this:

```text
$ kill 5918
```

After you press Enter (or perhaps press Enter again), the shell might report

```text
[1]+  Terminated             xosview
```

Note that users can kill only their own processes, but root can kill them all. Controlling any other running process requires root permission, which should be used judiciously (especially when forcing a kill by using the -9 option); by inadvertently killing the wrong process through a typo in the command, you could bring down an active system.

## Using the kill Command to Control Processes

The kill command is a basic UNIX system command. We can communicate with a running process by entering a command into its interface, such as when we type into a text editor. But some processes (usually system processes rather than application processes) run without such an interface, and we need a way to communicate with them, too, so we use a system of signals. The kill command accomplishes that by sending a signal to a process, and we can use this to communicate with any process. The general format of the kill command is as follows:

```text
# kill option PID
```

A number of signal options can be sent as words or numbers, but most are of interest only to programmers. One of the most common ones you will use is this:

```text
$ sudo kill PID
```

This tells the process with PID to stop; you supply the actual PID.

```text
$ sudo kill -9 PID
```

is the signal for kill (9 is the number of the SIGKILL signal); use this combination when the plain kill shown previously does not work:

```text
$ sudo kill -SIGHUP PID
```

is the signal to “hang up”—stop—and then clean up all associated processes, too. (Its number is 1.)

As you become proficient at process control and job control, you will learn the utility of a number of kill options. You can find a full list of signal options in the signal man page.

## Using Priority Scheduling and Control

Every process cannot make use of the system’s resources (CPU, memory, disk access, and so on) as it pleases. After all, the kernel’s primary function is to manage the system resources equitably. It does this by assigning a priority to each process so that some processes get better access to system resources and some processes might have to wait longer until their turn arrives. Priority scheduling can be an important tool in managing a system supporting critical applications or in a situation in which CPU and RAM usage must be reserved or allocated for a specific task. Two legacy applications included with Ubuntu are the nice and renice commands. (nice is part of the GNU sh-utils package, whereas renice is inherited from BSD UNIX.)

The nice command is used with its -n option, along with an argument in the range of -20 to 19, in order from highest to lowest priority (the lower the number, the higher the priority). For example, to run the xosview client with a low priority, use the nice command like this:

```text
$ nice -n 12 xosview &
```

The nice command is typically used for disk- or CPU-intensive tasks that might be obtrusive or cause system slowdown. The renice command can be used to reset the priority of running processes or control the priority and scheduling of all processes owned by a user. Regular users can only numerically increase process priorities (that is, make tasks less important) using this command, but the root operator can use the full nice range of scheduling (-20 to 19).

System administrators can also use the time command to get an idea about how long and how much of a system’s resources will be required for a task, such as a shell script. (Here, time is used to measure the duration of elapsed time; the command that deals with civil and sidereal time is the date command.) This command is used with the name of another command (or script) as an argument, as follows:

```text
$ sudo time -p find / -name core -print
/dev/core
/proc/sys/net/core
```
