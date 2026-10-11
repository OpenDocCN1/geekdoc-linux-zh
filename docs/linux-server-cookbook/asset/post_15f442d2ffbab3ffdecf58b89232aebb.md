
regular process has as a default *nice* value 0. Negative values (higher priority) can be only specified by administrators.

The option -l for the command **ps** and the command **top** shows the priority and the *nice* value for the processes running. This section will focus on how to change the *nice* values for a process.

*Figure 5.66* shows the example output for command **ps** with option -l to show the *priority* and the *nice* values:

```
agonzalez@ubuntu:~$ ps -l -q $(pidof top)
F S  UID   PID  PPID C PRI  NI ADDR SZ WCHAN     TTY          TIME CMD
0 S 1000 26798 26628 0  80  0 - 2723 do_sel pts/1    00:00:00 top
```

*Figure 5.66: Output example listing priority and nice value.*

The command **top** with the option -p and the **pid** will filter to that process and it would show the following example as shown in *figure 5.67*:

```
top - 16:19:09 up 11 days, 22:38,  2 users,  load average: 0.00, 0.00, 0.00
Tasks:  1 total,   0 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  3925.7 total,  1534.6 free,   253.0 used,  2138.1 buff/cache
MiB Swap:  2244.0 total,  2244.0 free,     0.0 used.  3379.7 avail Mem

    PID USER     PR  NI  VIRT   RES  SHR S  %CPU  %MEM  TIME+ COMMAND
   26798 agonzal+  20   0 10892  3900 3212 S   0.3   0.1  0:00.41 top
```

*Figure 5.67: Output example for the command top showing priority and nice value.*

The command **ps** would show the priority as a 100-*nice value* and the command *top* as a 20+*nice value*.

The command *nice* allows to execute commands with different *nice value*, and the command *renice* allows to change of the *nice value* for a running process. *Figures 5.68* to *5.69* show some examples using those commands:

- Run the command **sleep** with a different *nice value* (lower priority value):

```
agonzalez@ubuntu:~$ nice -n 15 sleep 600 &
[1] 26907

agonzalez@ubuntu:~$ ps -l -q $(pidof sleep)
F S  UID   PID  PPID C PRI  NI ADDR SZ WCHAN    TTY          TIME CMD
0 S 1000 26907 20949 0  95  15 - 1547 hrtime pts/0  00:00:00 sleep
```

*Figure 5.68: Example using command nice*

- Change *nice value* for a running process. As regular users only decreased *nice value* is allowed:

```
agonzalez@ubuntu:~$ renice -n 16 $(pidof sleep)
26907 (process ID) old priority 15, new priority 16
agonzalez@ubuntu:~$ ps -l -q $(pidof sleep)
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
0 S 1000 26907 20949 0 96 16 - 1547 hrtimer pts/0 00:00:00 sleep
```

*Figure 5.69: Example using command renice*

## Conclusion

Managing files, directories, and processes are required knowledge of administrating and using Linux systems. This chapter covered all the basics and more advanced options related to create and manipulate files and directories using system tools.

File and directory permissions are an important fact to protect files and directories to unwanted access. Different tools were described to assign user and group owners and permissions to files and directories.

Popular file editors and file managers were described to demonstrate the use of different tools to edit files, create directories, and navigate through different directories in the system.

Processes in Linux were described, and the importance of the priority when a process is executed and commands to modify the default priority were shown.

## Key facts

- Linux have a default layout directory structure.
- Each file and directory have three permissions: read, write and execute.
- Permissions for files and directory can be set to the user owner, group owner or to others.
- Multiple commands are available for formatting the output.
- There are available multiple useful file editors and file managers.

## Questions

1. What system directory keeps the system logs?
   1. /var/log/
   2. /tmp/
   3. /sys/log

2. What octal representation corresponds to u=rwx, g=rwx, o=rx?
   1. 664
   2. 775
   3. 777

3. What command is used to count lines, words, and characters?
   1. wc
   2. count
   3. sed

4. Using normal mode in VI(M) how to exit discarding the changes?
   1. :x
   2. :wq
   3. :q!

5. What range is valid for nice value?
   1. -20 to 19
   2. -19 to 20
   3. 0 to 100

## Answers

1. 1
2. 2
3. 1
4. 3
5. 1

# CHAPTER 6

**Monitoring System Resources**

# **Introduction**

This chapter covers how to monitor the system resources in a Linux system. It will introduce how the CPU and memory work in modern systems and the common tools available to check the status with the objective to do troubleshooting in case of issues or overload.

Other important resources to monitor to avoid downtimes in applications is the disk usage and the available space. Different tools will be described to check the current status and to detect the physical state of the disks.

Monitoring the networking became one of the most important tasks in Linux systems, especially with the introduction of complex networking in the systems to provide connectivity for virtual machines and containers.

The last part of the chapter focuses on disk quotas and resource limits and helping to protect the system when it is accessible by regular users to avoid the resources getting exhausted.

# **Structure**

In this chapter, we will discuss the following topics:

- Monitoring CPU resources
- Monitoring memory resources
- Monitoring disk usage and available space
- Monitoring network resources
- Quotas and limits

# **Monitoring CPU resources**

A **Central Processing Unit (CPU)**, a processor, executes instructions received from the system. In modern systems, there are three important concepts that are needed to understand, to be able to monitor and interpret the data received from the tools:

- CPU Socket (CPU slot): is a mount on a computer *motherboard* that accepts a CPU chip.
- CPU Core: a separate processing unit that reads and executes instructions. In modern systems, a *CPU* contains several cores.
- CPU Thread: A *thread* is a queue for an operating system instruction. Modern systems enable *hyper-threading* enabling two threads.

For example, if a system has two sockets, with four cores for each CPU, and has enabled the *hyper-threading*, it would have available eight cores and 16 threads. It is capable of running eight operating system instructions per cycle but would be able to have a *queue* of up to 16 tasks per cycle.

An advanced concept for physical servers is named **Non-Uniform Memory Access (NUMA)**. This architecture divides the memory into local and remote memory relative to the processors. CPU accessing the local memory assigned has better performance than accessing the remote access using an *interconnect*. *Figure 6.1* shows a representation of a node with two NUMA with one CPU socket and four cores each:

![](img/863afa537de4eed7deb11978bfbfa90e_186_0.png)

## Obtaining CPU(s) information

The command `lscpu` described in *Chapter 3, Using the Command Line Interface*, shows the important information related to the CPU socket, core, threads, and NUMA. *Figure 6.2* shows a node with two CPU sockets and eight cores per socket.

```
[root@server ~]# lscpu|grep --color=never -E "^(CPU\(|Thread|Core|Socket|NUMA)" CPU(s): 32 Thread(s) per core: 2 Core(s) per socket: 8 Socket(s): 2 NUMA node(s): 2 NUMA node0 CPU(s): 0-7,16-23 NUMA node1 CPU(s): 8-15,24-31
```

*Figure 6.2: Using command lscpu to obtain CPU information.*

The command **lstopo-no-graphics** part of the package **hwloc** provides a great visualization of the NUMA architecture and the association between CPUs and local memory. *Figure 6.3* illustrates an output example of this command for the same server as *figure 6.2*:

![](img/863afa537de4eed7deb11978bfbfa90e_187_0.png)

*Figure 6.3: Output example for the command lstopo-no-graphics.*

The file `/proc/cpuinfo` contains the list of all processors (*core/thread*) with a detailed information for each one. *Figure 6.4* shows an example using **grep**, **sort**, and **uniq** to create a report of how many CPUs are in each socket:

```
[root@server ~]# grep "physical id" /proc/cpuinfo |sort|uniq -c 16 physical id : 0 16 physical id : 1
```

*Figure 6.4: Getting information from file /proc/cpuinfo*

Other example commands to get processor information are as follows:

- *lshw -class processor* (*lshw -class processor -short*)
