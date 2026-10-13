# Performance Analysis Tools and Processes

Linux treats each task performed on your system as a process, which is assigned a number and a name. You can examine these processes and even stop them. Red Hat provides several tools for examining processes as well as your system performance. Easy monitoring is provided by several GUI tools, like Red Hat's Procman System Monitor.

# ps Command

From the command line, you can use the `ps` command to list processes. With the `-aux` option, you can list all processes. Piping the output to a `grep` command with a pattern enables you to search for a particular process. A pipe funnels the output of a preceding command as input to a following command. The following command lists all X Window System processes:

```
ps -aux | grep 'X'
```

A number of utilities on your system provide detailed information on your processes, as well as other system information such as CPU and disk use (see Table 27-10). Although these tools were designed to be used on a shell command line, displaying output in text lines, several now have KDE and GNOME versions that provide a GUI interface for displaying results and managing processes.

Table 27-10: Performance Tools

| Performance Tool | Description |
|---|---|
| vmstat | Performance of system components |
| top | Listing of most CPU intensive processes |
| free | Listing of free RAM memory |
| sar | System activity information |
| iostat | Disk usage |
| Procman System Monitor | Red Hat system monitor for processes and usage monitoring (System Monitor on System Tools menu). |
| KDE Task Manager and Performance Monitor | KDE system monitor for processes and usage monitoring |

# vmstat, free, top, iostat, Xload, and sar

The `vmstat` command outputs a detailed listing indicating the performance of different system components, including CPU, memory, I/O, and swap operations. A report is issued as a line with fields for the different components. If you provide a time period as an argument, it repeats at the specified interval-usually a few seconds. The `top` command provides a listing of the processes on your system that are the most CPU intensive, showing what processes are using most of your resources. The listing is in real time and updated every few seconds. Commands are provided for changing a process's status, such as its priority.

The `free` command lists the amount of free RAM memory on your system, showing how much is used and how much is free, as well as what is used for buffers and swap memory. `Xload` is an X Window System tool showing the load, CPU, and memory. `iostat` displays your disk usage, and `sar` shows system activity information.

# Procman System Manager

The current version of Red Hat provides the Procman System Manager for displaying system information and managing system processes, accessible from System Tools | System Monitor. There are two panels, one