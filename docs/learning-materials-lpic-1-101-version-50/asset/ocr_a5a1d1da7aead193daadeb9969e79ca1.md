```
$ ps -e -o user,uid,comm,tty,pid,ppid,prl,pmem,pcpu --sort=-pcpu | head
```

# # Process Niceness

Every normal process begins with a default nice value of 0 (priority 120). The *nice* name comes from the idea that “nicer” processes allow other processes to run before them in a particular execution queue. Nice numbers range from -20 (less nice, high priority) to 19 (more nice, low priority). Linux also allows the ability to assign different nice values to threads within the same process. The **NI** column in **ps** output indicates the *nice* number.

Only the root user can decrease the niceness of a process below zero. It’s possible to start a process with a non-standard priority with the command **nice**. By default, **nice** changes the niceness to 10, but it can be specified with option **-n**:

```
$ nice -n 15 tar czf home_backup.tar.gz /home
```

In this example, the command **tar** is executed with a niceness of 15. The command **renice** can be used to change the priority of a running process. The option **-p** indicates the PID number of the target process. For example:

```
# renice -10 -p 2164
2164 (process ID) old priority 0, new priority -10
```

The options **-g** and **-u** are used to modify all the processes of a specific group or user, respectively. With **renice +5 -g users**, the niceness of processes owned by users of the group *users* will be raised in five.

Besides **renice**, the priority of processes can be modified with other programs, like the program **top**. On the top main screen, the niceness of a process can be modified by pressing **r** and then the PID number of the process:

```
top - 11:55:21 up 23:38, 1 user, load average: 0,10, 0,04, 0,05
Tasks: 20 total, 1 running, 19 sleeping, 0 stopped, 0 zombie
%Cpu(s): 0,5 us, 0,3 sy, 0,0 ni, 99,0 id, 0,0 wa, 0,2 hi, 0,0 si, 0,0 st
KiB Mem : 4035808 total, 774700 free, 1612600 used, 1648508 buff/cache
KiB Swap: 7999828 total, 7738780 free, 261048 used. 2006688 avail Mem
PID to renice [default pid = 1]
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
1 root 20 0 74232 7904 6416 S 0,000 0,196 0:00.12 systemd
```