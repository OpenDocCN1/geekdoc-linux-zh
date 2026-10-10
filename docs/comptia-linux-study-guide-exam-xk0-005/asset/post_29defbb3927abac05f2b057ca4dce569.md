
addresses in a router, employ the `arp` or `ip neigh` command. To research slow or incorrect name server responses, the `host`, `dig`, `nslookup`, and `whois` utilities help.

**Summarize potential disk problems and solutions.** The `du` and `df` utilities help in preventing the system from running out of filesystem space and with troubleshooting when it does. If it is a logical volume, employ the LVM tools to add additional space when needed. I/O wait times, which may slow overall system performance, are seen with the `iostat` command. Changing a system’s I/O scheduler may help relieve this problem. The `topping` utility tests a disk to determine if it is usable for a particular application. To repair an ext* filesystem, use the `fsck` command. The `partprobe` command works well for newly created partitions in that it forces a reread of a disk’s partition table without rebooting the system.

**Clarify CPU troubleshooting procedures.** It is important to understand your system’s current processors’ information, which you can find in the `/proc/cpuinfo` file. To view CPU usage, employ the `uptime` and/or the `sar` commands. If needed and appropriate, you can tweak kernel parameters related to processor handling using the `sysctl` utility.

**Explain memory problems and solutions.** To view detailed system RAM information, look at the `/proc/meminfo` file’s contents. If your system does not have properly sized memory, you can see high RAM usage via the `free` command. In addition, the `vmstat` tool allows you to view disk I/O specific to swapping, which increases when RAM is improperly sized. If you need to add additional swap space, the `mkswap` utility will “format” a partition/file into swap, and the `swapon` command will put it into swap space. If you need to uncouple a partition/file from swap space, use the `swapoff` utility. If memory use hits critical levels, the kernel releases the OOM killer, which kills off particular processes to bring memory usage back to reasonable levels. Memory management can be modified using certain kernel parameters and the `sysctl` tool.

# Review Questions

1. Which of the following is true concerning network sockets? (Choose all that apply.)
    - A. Numbers used to identify which service is transmitting data
    - B. A single endpoint of a network connection’s two endpoints
    - C. Uses a combination of an IP address and a port number
    - D. Endpoints between processes on a local system
    - E. Provides better IPC than localhost

2. The system administrator, Preston, has noticed that the IPv4 network seems sluggish. He decides to run some tests to check for high latency. Which of the following utilities should he use? (Choose all that apply.)
    - A. `iperf`
    - B. `ping`
    - C. `ip neigh`
    - D. `dig`
    - E. `tracroute`

3. Scott has formulated a problem cause theory that routers are saturated with traffic and dropping TCP packets from their queues. Which of the following tools should he employ to test this theory? (Choose all that apply.)
    - A. `mtr`
    - B. `ifconfig`
    - C. `ethtool -s`
    - D. `tracepath`
    - E. `tracroute`

4. The network engineer, Keenser, believes the choices of name servers in the system’s `/etc/resolv.conf` file are inefficient. Which of the following tools can he employ to test new server choices?
    - A. `dnsmasq`
    - B. `whois`
    - C. `nmap`
    - D. `nslookup`
    - E. `ipset list`

5. Mera, a Linux system admin, believes a new application on her system is producing too much I/O for a particular partition, causing the system's processor to appear sluggish. Which tool should she use to test her problem cause theory?
    - A. iostat
    - B. ioping
    - C. du
    - D. df
    - E. iotop

6. From analysis, Arthur believes the system's I/O throughput will improve by changing the I/O scheduler. On his system is a real-time application, which uses a database located on a solid-state drive. Which I/O scheduler should Arthur choose?
    - A. scheduler
    - B. deadline
    - C. queue
    - D. cfq
    - E. noop

7. Using the `uptime` command, you will see CPU load averages in what increments? (Choose all that apply.)
    - A. 1 minute
    - B. 5 minutes
    - C. 10 minutes
    - D. 15 minutes
    - E. 20 minutes

8. Mary wants to view her system's processor performance over time. Which is the best utility for her to employ?
    - A. uptime
    - B. sysstat
    - C. sar
    - D. cat /proc/cpuinfo
    - E. sysctl

9. Gertie needs to determine a swap space element's type, name, and priority. Which command should she use?
    - A. vmstat
    - B. free
    - C. fstab
    - D. swapon
    - E. swapon -s

10. Elliot is administering a Linux system that has multiple swap spaces. One is on a logical volume, but it needs more space to accommodate additional RAM that is to be installed in the near future. What is the best way for Elliot to add swap space?
    - A. Add a partition and format it with the mkswap command.
    - B. Add a file and format it with the mkswap command.
    - C. Add a partition using the swapon utility.
    - D. Add a file using the swapon utility.
    - E. Use LVM tools to increase the logical volume.

# Chapter 21

# Optimizing Performance

- Objective 1.4: Given a scenario, configure and use the appropriate processes and services.
- Objective 4.3: Given a scenario, analyze and troubleshoot central processing unit (CPU) and memory issues.

![](img/c0a399aca0d18f8822d714ad0a173123_672_0.png)

![](img/c0a399aca0d18f8822d714ad0a173123_673_0.png)

This chapter discusses how Linux handles applications running on the system. Linux must keep track of lots of different programs, all running at the same time. Your goal as the Linux administrator is to make sure everything runs smoothly. This chapter shows just how Linux keeps track of all the active programs and how you can peek at that information. You’ll also see how to use command-line tools to manage the programs running on your Linux system.

# Looking at Processes

At any given time a large number of active programs are running on the Linux system. Linux calls each running program a process. A process can run in the foreground, displaying output on a console display or graphical desktop window, or it can run in the background, working on data behind the scenes. The Linux system assigns each process a process ID (PID) and manages how the process uses memory and CPU time based on that PID.

When a Linux system first boots, it starts a special process called the init process. The init process is the core of the Linux system; it runs scripts that start all the other processes running on the system, including the processes that start the text consoles and graphical windows you use to log in (see Chapter 6, “Maintaining System Startup and Services”).

You can watch just which processes are currently running on your Linux system by using the ps command. The default output of the ps command looks like this:

```
$ ps
  PID TTY          TIME CMD
 2797 pts/0    00:00:00 bash
 2884 pts/0    00:00:00 ps
$
```

By default, the ps command only shows the processes that are running in the current user shell. In this example, we only had the command prompt shell running (Bash) and, of course, the ps command itself.

The basic output of the ps command shows the PID assigned to each process, the terminal (TTY) that they were started from, and the CPU time that the process has used.

The tricky feature of the ps command (and what makes it so complicated) is that at one time there were two versions of it in Linux. Each version had its own set of command-line parameters controlling the information it displayed. That made switching between systems somewhat complicated.

Recently, the GNU developers decided to merge the two versions into a single ps program, and of course, they added some additional parameters of their own. The current ps program used in Linux supports three different styles of command-line parameters:

- Unix-style parameters, which are preceded by a dash
- BSD-style parameters, which are not preceded by a dash
- GNU long parameters, which are preceded by a double dash

This makes for lots of possible parameters and options to use with the ps command. You can consult the ps man page to see all the possible parameters that are available. Most Linux administrators have their own set of commonly used parameters that they remember for extracting pertinent information. For example, if you need to see every process running on the system, use the Unix-style –ef parameter combination, like this:

```
$ ps -ef
UID  PID  PPID C STIME TTY  TIME CMD
root     1     0  0 09:02 ?  00:00:02 /sbin/init
root     2     0  0 09:02 ?  00:00:00 [kthreadd]
root     3     0  0 09:02 ?  00:00:00 [ksoftirqd/0]
root     4     2  0 09:02 ?  00:00:00 [kworker/0:0]
root     5     2  0 09:02 ?  00:00:00 [kworker/0:0H]
root     6     2  0 09:02 ?  00:00:00 [kworker/u2:0]
root     7     2  0 09:02 ?  00:00:02 [rcu_sched]
root     8     2  0 09:02 ?  00:00:01 [rcuob/0]
root     9     2  0 09:02 ?  00:00:00 [rcuob_bh]
root    10     2  0 09:02 ?  00:00:00 [rcuob/0]
...
$
```

This format provides some useful information about the processes running:

**UID**: The user responsible for running the process

**PID**: The process ID of the process

**PPID**: The process ID of the parent process (if the process was started by another process)

**C**: The processor utilization over the lifetime of the process

**STIME**: The system time when the process was started

**TTY**: The terminal device from which the process was started

**TIME**: The cumulative CPU time required to run the process

**CMD**: The name of the program that was started in the process

Also notice in the –ef output that some process command names are shown in brackets. That indicates processes that are currently swapped out from physical memory into virtual
