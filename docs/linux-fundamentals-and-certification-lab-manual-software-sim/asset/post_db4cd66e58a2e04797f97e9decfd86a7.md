
## MORE ADMINISTRATIVE TASKS

- **no options** Shows your own currently running processes.

```text
# ps
  PID TTY          TIME CMD
12429 pts/1    00:00:00 su
12430 pts/1    00:00:00 bash
12485 pts/1    00:00:00 ps
```

- **u** This option shows the same information as no options, but with more detail.

```text
# ps u
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root      12429  0.0  0.0  4088   944 pts/1    S    10:12   0:00 [su]
root      12430  0.0  0.1  4344  1424 pts/1    S    10:13   0:00 -bash
root      12488  0.0  0.0  2616   676 pts/1    R    10:35   0:00 ps u
```

- **a** The a option shows all processes that are running on a terminal. The following list shows that su was run from jsmith's bash shell to connect as root.

```text
# ps au
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
jsmith    12395  0.0  0.1  4292  1376 pts/1    S    10:12   0:00 -bash
root      12429  0.0  0.0  4088   944 pts/1    S    10:12   0:00 [su]
root      12430  0.0  0.1  4344  1424 pts/1    S    10:13   0:00 -bash
root      12489  0.0  0.0  2624   684 pts/1    R    10:38   0:00 ps au
```

- **x** The x option will show all processes, even those not run from a terminal. The init process is the first process run on the Linux operating system. It spawns many processes when it starts and is the parent process of all processes. This option will show a lot of processes. You should either redirect it to a file or use the more filter. A partial list is presented as follows.

```text
# ps ax | more
  PID TTY          STAT   TIME COMMAND
    1 ?          S      0:27 init
    2 ?          SW     0:00 [migration/0]
    3 ?          SW     0:00 [migration/1]
    4 ?          SW     0:00 [khelperd]
```

- **l** The l option will give a long format.

```text
# ps axl | more
F   UID   PID  PPID PRI  NI  VSZ   RSS WCHAN   STAT TTY      TIME COMMAND
4     0     1     0   15   0  1384   488 schedu S    ?        0:27 init
5     0     2     0  -100  0     0     0 migrat SW   ?        0:00 [migration/0]
5     0     3     0  -100  0     0     0 migrat SW   ?        0:00 [migration/1]
1     0     4     1   15   0     0     0 contex SW   ?        0:00 [khelperd]
```

- **--user** or **-u** Use this GNU option to view the processes of any user.

```text
# ps --user jsmith
  PID TTY          TIME CMD
13071 ?        00:00:00 sshd
13072 pts/1    00:00:00 bash
```

You can combine -u with the l command to get a long listing of the processes.

```text
# ps -u jsmith l
F UID PID PPID PRI NI VSZ RSS WCHAN STAT TTY TIME COMMAND
5 501 16619 16617 15 0 6772 1804 schedu S ? 0:00 [sshd]
0 501 16620 16619 15 0 4300 1376 wait4 S pts/0 0:00 -bash
```

- **f** Lists a forest view. All processes are related in some way. The Linux operating system is started by running the init process, and all other processes are spawned from init. A forest view displays this relationship. The following is a partial listing of the forest.

```text
# ps axf | more
PID TTY STAT TIME COMMAND
1066 ? S 0:03 syslogd -m 0
1070 ? S 0:00 klogd -x
1088 ? S 0:00 [portmap]
1107 ? S 0:00 [rpc.statd]
1206 ? S 0:12 /usr/sbin/sshd
13766 ? S 0:00 \_ /usr/sbin/sshd
13768 pts/1 S 0:00 | \_ -bash
13882 ? S 0:00 \_ /usr/sbin/sshd
13884 pts/2 S 0:00 \_ -bash
13939 pts/2 R 0:00 \_\_ ps axf
13940 pts/2 S 0:00 \_ more
```

Another command that can be used to display a forest view is **pstree**. pstree can be used to view the entire tree of a PID, or of a user.

### Entire Forest:

```text
# pstree | more
init
|-atd
|-bdflush
|-crond
|-cupsd
|-esd
|-gdm-binary---gdm-binary-T X
| -gdmgreeter
|-gpm
|-kapmd
|-keventd
|-khubd
|-3*[kjournald]
|-klogd
|-kscan/DMA
|-kscan/HighMem
|-kscan/Normal
```

### Hierarchy of a Process:

```text
# pstree 1206
sshd--sshd---bash
\_sshd---bash---pstree
```

### Hierarchy of a Single User:

```text
# pstree dangle
sshd---bash---setup---printconf-tui
```

Knowing the options of ps is useful; however, some practical examples will help your understanding.

To list all processes owned by the oracle user: `ps -fu oracle`

To list process info for a specific process ID: `ps -fp pid`.

To kill all processes owned by apache: `ps -fu apache | awk '{print $2}' | xargs kill`

To list processes sorted by elapsed time since the process started: `ps -eo etime,pid,args | sort -rn`

## Using top

The **top** command provides a dynamic look at the processes of a Linux system. By default, top will run continuously. It not only shows running processes, but displays information about uptime, system memory usage, and swap usage. One of the key features of top is that it is interactive, meaning that it accepts commands to change the display, kill processes, and change priority.

The question mark (?) displays a list of valid commands. The man top command displays information about available commands as well.

```text
11:44:45  up 22 days,  59 min,   4 users,  load average: 0.04, 0.03, 0.02
96 processes:  95 sleeping,  1 running,  0 zombie,  0 stopped
CPU0  states:  0.3% user   0.0% system   0.0% nice   0.0% iwait  99.2% idle
CPU1  states:  0.0% user   0.3% system   0.0% nice   0.0% iwait  99.2% idle
Mem:  1030344k av, 1005228k used,  25116k free,  0k shrd,  132544k buff
      652164k actv,  564k in_d,  21088k in_c  706776k cached

Swap: 2040244k av,  42984k used, 1997260k free

  PID  USER     PRI   NI  SIZE  RSS SHARE STAT %CPU %MEM   TIME CPU COMMAND
 14128 root     15  0  1152  1152  872 R    0.0  0.1   0:00  0 top
 14127 jsmith   25 10  1376  1376 1184 S    0.0  0.1   0:12  1 blaster
 14059 dngle    15  0  1344  1344 1072 S    0.0  0.1   0:00  1 bash
 14058 dngle    15  0  1828  1768 1436 S    0.0  0.1   0:00  1 sh
 14054 jsmith   15  0  7048  6968 5676 S    0.0  0.6   0:00  0 notification-
 14048 root     15  0   484   484  428 S    0.0  0.0   0:00  1 pam_timestamp
 14047 jsmith   15  0 13296  12M 8592 S    0.0  1.2   0:55  1 rhn-applet-gu
 14045 jsmith   15  0  4232  4232 3536 S    0.0  0.4   0:00  1 pam-panel-ico
 14043 jsmith   15  0  6812  6812 5636 S    0.0  0.6   0:01  1 eggcups
 14041 jsmith   15  0  6060  6056 5040 S    0.0  0.5   0:00  1 magicdev
 14039 jsmith   15  0 15996  15M 9064 S    0.0  1.5   0:03  1 nautilus
 14037 jsmith   15  0 10940  10M 8232 S    0.0  1.0   0:01  1 gnome-panel
 14033 jsmith   15  0  5852  5848 4740 S    0.0  0.5   0:00  1 metacity
 14030 jsmith   15  0  1772  1772 1436 S    0.0  0.1   0:00  0 xscreensaver
 14025 jsmith   15  0  1188  1188  996 S    0.0  0.1   0:00  1 fam
```

In this listing of the **top** command, the up time is 22 days, and there are 4 users and 96 processes. It lists free memory as 25,116k and free swap as 199,726k. The process list is similar to that of the **ps** command.

The k command in top will delete a process. A careless moment when using this command can cause serious problems. Starting in secure mode eliminates the possibility of accidentally killing a process. To start in secure mode, use the **top -s** command.

Secure mode looks and acts the same as normal mode; however, if you use the k command you will receive the message “Can’t kill in secure mode.”

A useful option for top is the “-n” option. The command `top -n 1 >> /top.file` will save the output of one top iteration to the file top.file. This is a convenient way to collect system performance information over a long period of time. This command can be automated and controlled via cron.

If you are using KDE or GNOME, a graphical display for processes can be displayed. The same actions and fields are available as in the command-line tool (Figure 11-6).

The graphical tool offers a graphical view of CPU and memory/swap usage (Figure 11-7). Properties can be set to select the fields to display, the update interval, and others.

![](img/37f079cee226b270f2e09b37a2e4a05d_311_0.png)

FIGURE 11-6  
GNOME process listing.

![](img/37f079cee226b270f2e09b37a2e4a05d_311_1.png)

FIGURE 11-7  
GNOME system monitor:

## Prioritizing Processes

As mentioned earlier in this chapter, processes have priority values assigned to them. A process's priority determines how much CPU time it has available. Linux is multitasking, meaning that it can run more than one task at a time. On most Linux systems, however, there is only one CPU. Processes that are executed on these systems have to take turns using resources. Even on multiprocessor systems, so many processes are running at any given time that they still must share CPU resources according to their priority.

Two commands are used in the Linux operating system to assign priority—nice and renice. The nice command executes commands with specific priority levels. The renice command changes the priority level of processes that are already running. Priorities can also be changed using top or GNOME System Monitor.

The range of priority values is from -20 (the highest) to 19 (the lowest). The syntax of nice is nice [options] command, where the options are -n or --adjustment. To start a program called sniffer with a starting priority of 10, use the nice -n 10 sniffer command.
