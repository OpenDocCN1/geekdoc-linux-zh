Either the `select()` or the `poll()` system calls provide the power to monitor several channels at the same time. With good planning, you can avoid some of the overhead problems multitasking encounters.

# Implementing Timeouts

A simple alternative to polling I/O channels is to tell the operating system that you do not want to wait longer than a specified time. The Linux system calls do not provide a direct way of doing this. Consider using these ways to implement timeouts:

+   - With the timeout in the `select()` or `poll()` system call
+   - With a signal (SIGNALRM) to wake up the task

![](bbox=[0.13, 0.37, 0.91, 0.48])

The `select()` and `poll()` system calls (described previously) supply a timeout parameter in microseconds. Using these system calls is perhaps the easiest way to implement timeouts, but the timeouts apply to all channels in the call.

This situation can be a problem: Suppose you have three channels, and one of them is not very responsive. Using just these system calls, you cannot detect that the failing channel should have timed out and closed. You can manually keep individual times for each channel, resetting the time with each response. Still, that may be a lot of unnecessary checking and logging.

You can use an alternative instead: an alarm signal. An *alarm* is a clock that runs in the kernel. When the alarm goes off, the kernel sends a wakeup call to the task in the form of a signal. If the task is waiting in a system call, the signal interrupts the call, the task enters the signal handler, and then the system call returns with an EINTR error.

Every task can send itself a signal, but the task needs to know what to do with the signal. On some systems, the sleep library call uses the `alarm()` system call, first setting up the task to capture the SIGALRM signal. Please look at the following example:

```
```c
/***** ****************************************************** /****
/*** Example: Timeout example using the alarm() system   ***/
/*** call. (Excerpt from echo-timeout.c on CD.)       ***/
/***** ****************************************************** /****
...
```
```