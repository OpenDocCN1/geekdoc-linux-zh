```
printf("Hello, world!\n");
exit(0);
}
% gcc48 -w dup2.c -o dup2
% ./dup2 foo
% cat foo
Hello, world!
%
```

You can redirect standard input (or standard error) in the same manner as discussed. All three standard files may be redirected to one file or multiple files, one each for standard input, standard output, and standard error.

# EXERCISE 19.14

Replicate the preceding sessions on your system. Do the dup.c and dup2.c programs work as expected?

# 19.5 GETTING THE ATTENTION OF A PROCESS: UNIX SIGNALS

Similar to how a peripheral device may use an interrupt to get the attention of the CPU and be served, you may use a signal to get the attention of a process. We discussed this topic in detail in Chapters 13 and 15 to explain signal/interrupt handling in shell scripts. Here, we discuss signal handling in a C program.

# 19.5.1 What Is a Signal?

As stated earlier, a signal in UNIX vocabulary is an event that interrupts the execution of a process. We discussed the events that cause signals in Chapter 13, Section 13.4 while discussing advanced Bourne Shell programming. Some of the events that cause signals are listed in Table 13.1. We reproduce that table here as Table 19.8.

You can view the complete list of events that cause signals by viewing the man pages for the kill command or kill() system call. You can also use the kill -l command to display the list of signals. A similar list is also found in the /usr/include/sys/signal.h file.

You can send a signal to a process by using the kill command or the kill() system call. Both take two arguments, a signal number and the PID of the process to receive the signal. For example, the kill -16 12345 command sends signal number 16 to the process with PID 12345.

# 19.5.2 Intercepting Signals

A process may use the sigaction() system call or the signal() library call to intercept a signal and take one of the following three possible actions:

+   1. Ignore the signal
+   2. Take the default action as defined by the kernel
+   3. Take the programmer-defined action