# Linux Administration: A Beginner's Guide

+   1, 9, and 15, which translate to hang-up process, kill process, and terminate process, respectively. 

When `kill` is invoked, it requires at least one parameter: the process identification number (PID) derived from the `ps` command.

# Signals

An optional parameter available for `kill` is `-n`, where `n` represents a signal number. If you don't specify the `-n` option, signal 15 will be by default. We'll discuss signals 1, 9, and 15 here.

The hang-up signal 1 (SIGHUP), is a bit of a throwback to the VT10 terminal days of UNIX. When a user's connection dropped in the middle of a session, all of that terminal's running processes would receive a SIGHUP (often called HUP). This signal gives the opportunity to perform a clean shutdown or, in the case of background processes, to ignore the signal. These days, a HUP is used to tell certain server applications to go reread their configuration files (you'll see this action in several of the later chapters).

The kill signal, 9 (SIGKILL), is impolite of stopping a process. Rather than asking a process to stop, the operating system simply kills the process. The only time this will fail is when the process is in the middle of a system call (as a request to open a file), in which case the process will die once it returns from the system call.

The kill signal, 15 (SIGTERM), can be used to request a process to gracefully terminate itself. When passed only the PID, `kill` sends signal 15 (SIGTERM) by default. Some programs intercept this signal and perform a number of actions so that they can shut down cleanly. Others just stop running in their tracks. Either way, SIGTERM isn't a guaranteed method for making a process stop.

# Security Issues

The ability to terminate a process is obviously a powerful one, thereby making security precautions important. Users may kill only processes they have permission to kill. If non-root users attempt to send signals to processes other than their own, error messages are returned. The root user is the exception to this limitation; may send signals to all processes in the system. Of course, this root needs to exercise great care when using the `kill` command.

# Examples Using the kill Command

![](bbox=[0.091, 0.768, 0.153, 0.808])

NOTE The following examples are arbitrary; the PIDs used are completely fictitious and will be different on your system.

Recall that when a signal to is not specified, SIGTERM (signal 15) will be sent by default. Use this command to terminate (signal 15) a process with PID number 205989.

```
[root@server ~]# kill 205989
```