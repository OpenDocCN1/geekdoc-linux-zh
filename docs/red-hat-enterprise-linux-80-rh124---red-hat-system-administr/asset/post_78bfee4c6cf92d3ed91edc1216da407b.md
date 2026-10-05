
# Monitoring and Managing Linux Processes

```
499 %CPU(s): 0.0 us, 0.0 sy, 0.0 ni, 100 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0
500 Mib 1829.4 total, 1428.7 free, 179.0 used, 221.8 buff/cache
501 Mib 1024.0 total, 1024.0 free, 0.0 used, 1492.1 avail Mem
PID USER PRIRT RESZ SHR %CPU %MEM TIME+ COMMAND
20723 student 20 0 222448 3016 2764 S 24.7 0.2 0:53.28 process102
1180 student 20 0 222448 3056 2068 S 12.0 0.2 0:51.06 process101
...output omitted..
```

> NOTE
If you do not see process101 at the top of the process list, press Shift+P to ensure that it is sorted by CPU utilization.

- 8. The load average is still below 1. Copy process101 to a new script called process103. Increase the addition count to eight hundred thousand. Start process103 in the background. It may take a few minutes for the load average to change.

- 8.1. In the right terminal shell, confirm that the load average is below 1.

```
top - 20:24:13 up 6:56, 2 users, load average: 0.43, 0.41, 0.29
...output omitted..
```

- 8.2. In the left terminal shell, use the cp command to copy process101 to a new script called process103.

- 8.3. In the left terminal shell, use the vim command to edit the process103 script. Increase the addition count to eight hundred thousand. Enter interactive mode using the key. Type: wq to save the file.

```
[student@serverb]$ vim process103
!/bin/bash
while true; do
	var=1
	while [[ $var -lt 800000 ]]; do
		var=$((var+1))
		done
	sleep 1
done
```

- 8.4. Start process103 in the background. The CPU usage hovers between 60% and 85%.

```
[student@serverb]$ process103
```

- 8.5. Confirm that all three jobs are running in the background.

```
[student@server bin]$ jobs
[1] Running       process101 &
[2]- Running       process102 &
[3]+ Running       process103 &
```

- 8.6. In the right window confirm that the load average is above 1.

top - 20:45:33 7:17, 2 users, load average: 1.10, 0.90, 0.64

- 9. In the left terminal shell, become root. Suspend the process101 process. List the remaining jobs. Observe that the state for process101 is now T.

- 9.1 Use the - command to become root. The password is redhat.

```
[student@server bin]$ su -
Password: redhat
```

- 9.2 Use the killall with the -SIGSTOP option to suspend the process101 process.

```
[root@server bin]## kill -SIGSTOP process101
```

- 9.3 In the left terminal shell that process101 is no longer running.

```
top - 20:52:01 7:24, 2 users, load average: 1.19, 0.89
Tasks: 112 total, 2 running, 110 sleeping, 0 stopped, 0 zombie
499% (CPU): 0.0 us, 0.0 sy, 0.0 ni, 100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
500 MiB Mem: 1829.4, 1428.7 free, 179.0 used, 221.8 buff/cache
501 MiB Swap: 1024.0, 1024.0, 0.0 used, 1492.1 avail Mem
PID PR NI VIRT STAT SHR %CPU %MEM TIME+ COMMAND
24043 20 0 222448 2974 R 66.1 0.2 6:59:50 process103
20723 20 0 222448 3016 2764 R 29.9 0.2 11:04:38 process102
...output omitted...
```

- 9.4 In the left terminal run the ps with the jt to view the remaining jobs. Note that process101 has a status of T. This denotes that the process is currently suspended.

```
[root@server bin]## ps jt
PP PID GID TTY TPGID STAT UID TIME COMMAND
...output omitted...
27138 1180 1180 21738 pts/0 28558 R 1000 3:06 /bin/bash /home/student/bin/process101
27138 20723 20723 21738 pts/0 28558 R 1000 1:23 /bin/bash /home/student/bin/process102
27138 24043 24043 21738 pts/0 28558 R 1000 0:35 /bin/bash /home/student/bin/process103
...output omitted...
```

- 10. Resume the process101.

- 10.1. In the left shell use the kill command with the -SIGCONT to resume the process101.

```
[root@server ~]# kill -SIGCONT process101
```

- 10.2. In the right terminal confirm that the process is running.

```
top - 20:57:02 7:29, 2 users, load average: 1.14 1.20 0.09
Tasks: 112 total, 2 running, 110 sleeping, 0 stopped, 0 zombie
%CPU(s): 0.0 us, 0.0 sy, 0.0 ni, 100.0 id, 0.0 wa, 0.0 hi, 0.0 si
Mib Mem: 1829.4, 1428.7 free, 179.0 used, 221.8 buff/cache
Mib Swap: 1024.0, 1024.0 free, 0.0 used, 1492.1 avail Mem
```

- 11. Terminate process102, process103 using the command. Confirm process102 and process103 no longer display in top.

- 11.1. In the left shell use the kill command terminate process101, process102 and process103.

```
[root@server ~]# kill process101
[root@server ~]# kill process102
[root@server ~]# kill process103
```

- 11.2. In the right terminal confirm that the processes no longer appear in top.

```
top - 21:05:06 7:37, 2 users, load average: 1.26 1.29 1.12
Tasks: 112 total, 2 running, 110 sleeping, 0 stopped, 0 zombie
%CPU(s): 0.0 us, 0.0 sy, 0.0 ni, 100.0 id, 0.0 wa, 0.0 hi, 0.0 si
Mib Mem: 1829.4, 1428.7 free, 179.0 used, 221.8 buff/cache
Mib Swap: 1024.0, 1024.0 free, 0.0 used, 1492.1 avail Mem
```

| PID | USER | PR | NI | VIRT | RES | SHR | %CPU | %MEM | TIME+ | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | root | 20 | 0 | 178536 | 13488 | 8996 | S | 0.0 | 0.7 | 00:01.21 | systemd |
| 2 | root | 20 | 0 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00.00 | kthread |
| 3 | root | 20 | -20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 00:00.00 | rcu_gp |
| st | | | | | | | | | | |

- 12. In the left terminal shell, exit from the root user. In the right terminal shell stop the top command. Exit from server in both windows.

- 12.1. Use the exit command to log out from the root user.

```
[root@serverb ~]# exit
logout
[1] Terminated         process101
[2] Terminated         process102
[3]- Terminated         process103
```

- 12.2. Exit from all terminal windows.

```
[student@serverb bin]$ exit
[student@workstation ~]$
```

- 12.3. In the right terminal shell, use the Ctrl+C command to quit. Use the exit command to log out.

```
[student@serverb ~]$ exit
logout
Connection to serverb closed.
[student@workstation ~]$
```

## Evaluation

On workstation, run the lab processes-review grade script to confirm success on this exercise.

```
[student@workstation ~]$ lab processes-review grade
```

## Finish

On workstation, run the lab processes-review finish script to complete the lab.

```
[student@workstation ~]$ lab processes-review finish
```

This concludes the lab.

## SUMMARY

In this chapter, you learned:

- A process is a running instance of an executable program, Processes are assigned a state, which can be running, sleeping, stopped, or zombie. The **ps** command is used to list processes.

- Each terminal is its own session and can have foreground process and independent background processes. The **jobs** command displays processes within a terminal session.

- A signal is a software interrupt that reports events to an executing program. The **kill**, **pkill**, and **killall** commands use signals to control processes.

- Load average is an estimate of how busy the system is. To display load average, you can use **top**, **uptime**, or **w**.

## CHAPTER 9

# CONTROLLING SERVICES AND DAEMONS

| GOAL | Control and monitor services using systemd. |
| :--- | :--- |
| OBJECTIVES | - List systememons and network services started by systemd and socket units.<br>- Control system services systemctl. |
| SECTIONS | - Identifying Automatically Started Processes (Guided Exercise)<br>- Controlling Services (Guided Exercise) |
| LAB | Controlling Services and Daemons |

## IDENTIFY AUTOMATICALLY STARTED PROCESSES

### OBJECTIVES

After completing this section, you should be able to list daemons and network services started by systemd and socket units.

### INTRODUCTION to systemd

The systemd daemon manages startup for Linux, including service startup. It activates system resources, daemons, and other processes both at boot time and on a running system.

Daemons are processes that either run in the background, performing various tasks. Generally, daemons start automatically at boot time and continue until shutdown or are manually stopped. It is a convention for many daemon programs to end in the letter d.

A service in the systemd often refers to one or more daemons, but starting or stopping a service may make a one-time change to the state of the system, which does not involve leaving a daemon running (called oneshot).

In Red Hat Linux, the first process that starts (PID 1) is systemd. A few of the features provided by systemd include:

- Parallelization capabilities (starting multiple services simultaneously), which increase the speed of a system.
- On-demand starting of daemons without requiring a separate service.
- Automatic service dependency management, which can prevent long timeouts. For example, a network-dependent service will not attempt to start until the network is available.
- A method of tracking related processes by using Linux control groups.

## DESCRIB SERVICE UNITS

systemd uses units to manage different types of objects. Some common unit types are listed below:

- Service units use a .service extension and represent system services. This type of unit is used to start frequently accessed daemons, such as a web server.
- Socket units have a .socket extension and represent inter-process communication (IPC) sockets that systemd monitor. If a client connects to the system, systemd will start a daemon and pass the connection to it. Socket units are used to delay the start of a service at boot time and to start frequently used services on demand.

- Path units have a .path extension and are used to delay the activation of a service until a specific file system change occurs. This is commonly used for services which use spool directories such as a printing system.

The systemctl command is used to manage units. For example, display available unit with the systemctl -t help command.
