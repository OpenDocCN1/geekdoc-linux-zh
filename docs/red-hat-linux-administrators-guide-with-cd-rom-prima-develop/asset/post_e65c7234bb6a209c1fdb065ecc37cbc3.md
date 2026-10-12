
in increased swap space consumption. Once the Netscape program is shut down swap space returns to normal levels.

## Monitoring a System's Load Using top

The top command does not show the current system state in a static format. Unlike ps, which simply takes a snapshot of your system at the moment the command is issued; top gives you a real-time analysis of all processes running at any given moment. The default refresh time is five seconds, but you can modify this setting depending upon how often you need updates. You change the refresh time as follows:

```
top d10
```

The *d* sets the next number as the interval between refresh screens in seconds. While top can be considered more memory-intensive than ps on systems with limited physical memory, you may use it as a secondary process to better track down rampant processes. This can further bog down the system if too many processes are running or if one process is already out of control. Its primary purpose is for debugging the system. The top command can also quickly show you what process might be out of control along with the necessary PID in order to shut the process down.

A nice feature of top is that it automatically updates itself. You can have a version of top running continuously in the background if constant supervision of the system is preferred or required. Be mindful that top is more CPU-intensive than that of ps. If you require an updated display of all processes on the system every few seconds, you may want to either lengthen the refresh times or run it periodically. This is yet another instance where you can set the *nice* value of a program quite low.

Figure 7.1 shows sample output of top as seen in a regular term window.

Like other commands, such as *uptime* and *ps*, top displays processes, system load, and the amount of time the system has been running. In fact, the very first line of top's output is identical to that of uptime. But the output also displays information not seen elsewhere. The top command's output states the exact number of processes and breaks them down in terms of those sleeping, actively running, zombied, and stopped. These figures are subject to change depending upon the number of programs running or the power of the CPU.

## Part II

# ADMINISTERING THE SYSTEM

![](img/a0884097af3186d9b4f616aaa3f065b0_263_0.png)

### FIGURE 7.1

The top command’s output lets you view not only the amount of time a system has been up, but also a running total of processes and their load on the system.

Next, top’s output displays the amount of CPU usage in the kernel. The output displays this as the percentage of the CPU that is in use by both the user and the kernel; the output also indicates the percentage of the CPU that is idle. This information can be useful if you are determining whether a problem lies with a user’s configuration or with the system itself. In the case of a daemon run amok, the system load would be much greater than that of the user’s utilization of the CPU.

The last few lines show the memory usage. Memory is normally divided between physical memory and swap memory. These lines show how much is normally available, how much is used, and how much is free. They also state the amount of shared and buffered memory on the system’s physical memory and the cached amount of physical memory currently being used by the buffer cache, i.e. caching disks.

The top command is a very practical utility to use when you are monitoring the processes currently running on a Linux machine. It provides ample information for determining the cause of system problems and can also render details about other processes that may need to be managed. The program will continue to run until you press the q key to quit.

Normally, top will sort the processes in order, with the most CPU-intensive process placed at the top. But you can also sort by memory and/or CPU use. The program automatically refreshes the screen every few seconds. A couple of the more frequently used options associated with top are sorting the output by either memory, typing M in the top display, or sorting by processor use, by typing P in the window. If you need to know the additional options that top accepts as input, entering a simple help query or pressing the h key will bring up a display that shows the various possibilities.

## Recognizing Commonly Used Signals

Signals are used to manipulate the processes either running or sleeping on the system. They enable users to tell the process to either drop what it is currently doing and do something else, or to reread a currently running file or process. The kernel handles some signals, such as kill -9, while others are managed by the program that first initiated the process. Most often the SIGHUP or HUP signal will make a daemon re-read its configuration files, but that is not always the case for some daemons. In either case, there are many types of signals. Each is used with the kill command.

You can use one of two methods to send signals to the system: either as a numeric value such as a -1 or a -9, or as a written request such as the hangup signal or -HUP command. This book will explore only a few signals closely. Most users need to know only a couple of signals FOR normal daily use, the -1 and -9 signals being the most frequently used.

Table 7.1 lists some of the more generic signals, along with their numeric value, their names, and their actions. The numbers in boldface do not apply to every system, including the various distributions of Linux, so it is possible that these signals will have different numbers than those listed.

A kill signal sent as -1 can also be sent as a -HUP command. As shown in the table, above every numbered kill command also is a name that can be used in lieu of the numbered command. When sending a signal to a process there are two elements that are needed to properly modify the process: the order (here the kill command), and the action (either a number or a signal name). A -1 or -HUP command will cause the program to reread its configuration files. It sends a hangup command, signaling the process to restart. This command is useful when you are changing configuration files such as httpd.conf for the web server and then want the server to reread the new configuration without stopping and restarting the daemon itself.

You can also slay any pesky process that is disrupting the system or that has stopped. To do so, you issue the kill -9 command with the process's PID.

### Table 7.1 A Brief Summary of Signals Used by the kill Command and Their Purpose

| Number | Name | Description | Default Action |
| :--- | :--- | :--- | :--- |
| 1 | SIGHUP | Hangup | Terminate |
| 2 | SIGINT | Interrupt | Terminate |
| 3 | SIGQUIT | Quit | Terminate |
| 4 | SIGILL | Illegal instruction | Terminate |
| 5 | SIGTRAP | Trace trap | Terminate |
| 6 | SIGIOT | IOT trap | Terminate |
| 7 | SIGEMT | EMT trap | Terminate |
| 8 | SIGFPE | Arithmetic exception | Terminate |
| 9 | SIGKILL | Kill | Terminate |
| 10 | SIGBUS | Bus error | Terminate |
| 11 | SIGSEGV | Segmentation fault | Terminate |
| 12 | SIGSYS | Bad system call | Terminate |
| 13 | SIGPIPE | Broken pipe | Terminate |
| 14 | SIGALRM | Alarm clock | Terminate |
| 15 | SIGTERM | Program termination | Terminate |
| 16 | SIGURG | Socket in extremis | Ignore |
| 17 | SIGSTOP | Stop | Stop |
| 18 | SIGTSTP | Keyboard stop | Stop |
| 19 | SIGCONT | Continue after stop | Ignore |
| 20 | SIGCHLD | Child status changed | Ignore |
| 21 | SIGTTIN | Invalid read | Stop |
| 22 | SIGTTOU | Invalid write | Stop |
| 23 | SIGIO | I/O possible on floppy | Ignore |
| 24 | SIGXCPU | CPU time limit up | Terminate |
| 25 | SIGXFSZ | File size limit up | Terminate |
| 26 | SIGVTALRM | Virtual time alarm | Terminate |
| 27 | SIGPROF | Profiling timer alarm | Terminate |
| 28 | SIGWINCH | Window changed | Ignore |
| 29 | SIGLOST | Resource lost | Terminate |
| 30 | SIGUSR1 | User-defined | Terminate |
| 31 | SIGUSR2 | User-defined | Terminate |
