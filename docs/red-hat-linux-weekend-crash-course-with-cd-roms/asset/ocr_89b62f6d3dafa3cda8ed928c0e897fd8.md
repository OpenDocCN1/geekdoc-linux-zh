is a sequential number assigned by the Linux kernel. Right at the beginning of the list of processes, you notice a process with a process ID (PID) of 1:

```
PID TTY   STAT   TIME COMMAND
1 ?       S       0:05 init [5]
```

As you can see, init is the first process and it has a PID (or process number) of 1. Also, init starts all other processes in your Linux system. That's why init is referred to as the *mother of all processes*.

What the init process starts depends on the following:

+   - The *run level*, which designates a system configuration in which only a selected group of processes exists
+   - The contents of the `/etc/inittab` file, a text file that specifies the processes to start at different run levels
+   - A number of shell scripts (located in the `/etc/rc.d` directory and its sub-directories) that are executed at a specific run level

The current run level, together with the contents of the `/etc/inittab` file, controls which processes init starts. Linux, for example, has seven run levels: 0, 1, 2, 3, 4, 5, and 6. By convention, some of these levels indicate specific processes that run at that level. Run level 1, for example, denotes a single-user, standalone system. Run level 0 means the system is halted, and run level 6 means the system is being rebooted. Run levels 2 through 5 are multiuser modes with various levels of capabilities.

The initial default run level is 3 for text-mode login screens and 5 for the graphical login screen. As the following section explains, you can change the default run level by editing a line in the `/etc/inittab` file.

To check the current run level, type the following command:

```
/sbin/runlevel
N 5
```

This command prints two alphanumeric characters as output. The first character of the output shows the previous run level (N means there was no previous run level), and the second character shows the current level (5).