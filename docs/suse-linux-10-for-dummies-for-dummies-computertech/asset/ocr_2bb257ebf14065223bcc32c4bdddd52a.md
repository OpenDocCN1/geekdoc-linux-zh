# # Starting and Stopping Services

Knowing the sequence in which Linux starts processes as it boots is important. You can use this knowledge to start and stop services, such as the Web server and Network File System (NFS). The next few sections provide you with an overview of how Linux boots and starts the initial set of processes. These sections also familiarize you with the shell scripts that start various services on a Linux system.

# ## Understanding how Linux boots

When Linux boots, it loads and runs the core operating system program from the hard drive. The core operating system is designed to run other programs. A process named *init* starts the initial set of processes on your Linux system.

To see the processes currently running on the system, type

```
```bash
ps ax | more
```
```

You get an output listing that starts off like this:

```
```
PID TTY       STAT    TIME COMMAND
  1   ?         S      0:01 init [5]
```
```

The first column, with the heading PID, shows a number for each process. PID stands for *process ID* (identifier) — a sequential number assigned by the Linux kernel. The first entry in the process list, with a *process ID* (PID) of 1, is the init process. It’s the first process, and it starts all other processes in your Linux system. That’s why init is sometimes referred to as the “mother of all processes.”

What the init process starts depends on the following:

+   - The *run level*, an identifier that identifies a system configuration in which only a selected group of processes are started.
+   - The contents of the `/etc/inittab` file, a text file that specifies which processes to start at different run levels.
+   - A number of shell scripts — sequence of Linux commands — that are executed at specific run levels.

SUSE Linux uses seven run levels — 0 through 6. Table 17-2 shows the meanings of the different run levels in SUSE Linux.