To list all processes owned by the oracle user: `ps -fu oracle`

To list process info for a specific process ID: `ps -fp pid`.

To kill all processes owned by apache: `ps -fu apache | awk ‘{print $2}’ | xargs kill`

To list processes sorted by elapsed time since the process started: `ps -eo etime,pid,args | sort -rn`

# Using top

The **top** command provides a dynamic look at the processes of a Linux system. By default, top will run continuously. It not only shows running processes, but displays information about uptime, system memory usage, and swap usage. One of the key features of top is that it is interactive, meaning that it accepts commands to change the display, kill processes, and change priority.

The question mark (?) displays a list of valid commands. The man top command displays information about available commands as well.

```
```
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
```

In this listing of the **top** command, the up time is 22 days, and there are 4 users and 96 processes. It lists free memory as 25,116k and free swap as 199,726k. The process list is similar to that of the **ps** command.

The k command in top will delete a process. A careless moment when using this command can cause serious problems. Starting in to secure mode eliminates the possibility of accidentally killing a process. To start in secure mode, use the **top -s** command.

Secure mode looks and acts the same as normal mode; however, if you use the k command you will receive the message “Can’t kill in secure mode.”

A useful option for top is the “-n” option. The command `top -n 1 >> /top.file` will save the output of one top iteration to the file top.file. This is a convenient way to collect system performance information over a long period of time. This command can be automated and controlled via cron.

If you are using KDE or GNOME, a graphical display for processes can be displayed. The same actions and fields are available as in the command-line tool (Figure 11-6).

The graphical tool offers a graphical view of CPU and memory/swap usage (Figure 11-7). Properties can be set to select the fields to display, the update interval, and others.