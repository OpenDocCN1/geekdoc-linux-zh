5. Unsurprisingly, it's most common to feed this output to grep, to weed out the specific information you seek. Curious about what processes are not running as root? Try this:

```
```bash
# ps -aux | grep -vE 'root'
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
rpc 706 0.0 0.1 1556 124 ? S 13:21 0:00 portmap
rpcuser 734 0.0 0.0 1596 4 ? S 13:21 0:00 rpc.statd
xfs 1051 0.0 0.3 5112 1492 ? S 13:22 0:09 xfs -droppriV -da
daemon 1087 0.0 0.0 1444 44 ? S 13:22 0:00 /usr/sbin/atd
```
```

Note that all of these are in sleep state (STAT=S). Indeed, a quick scan of the earlier output will reveal that the ps command is the only one in run state when the process snapshot was taken by ps.

6. If you're curious about what programs are consuming the most memory, rather than dig through ps, most versions of Unix include a very helpful utility called top (or, on some systems, monitor), which shows you all running applications, but refreshes the list every few seconds. You can also get top to dump its output to the screen and quit, rather than iteratively refresh. Then you can use head to identify the half dozen processes using the most CPU time:

```
```bash
# top -b -n0 | head -20
5:11pm up 3:50, 4 users, load average: 0.22, 0.09, 0.08
57 processes: 56 sleeping, 1 running, 0 zombie, 0 stopped
CPU states: 9.8% user, 5.4% system, 0.0% nice, 84.6% idle
Mem: 62264K av, 56172K used, 6092K free, 0K shrd, 1640K buff
Swap: 192772K av, 15208K used, 177564K free 18420K cached

PID USER PRI NI SIZE RSS SHARE STAT %CPU %MEM TIME COMMAND
9299 root 15 0 1032 1028 828 R 14.4% 1.6% 0:00 top
1281 root 9 0 3544 3148 2372 S 1.6% 5.0% 5:56 kdeinit
1254 root 9 0 1184 852 580 S 0.8% 1.3% 0:26 artsd
1 root 9 0 120 72 72 S 0.0% 0.1% 0:04 init
2 root 9 0 0 0 0 SW 0.0% 0.0% 0:00 keventd
3 root 9 0 0 0 0 SW 0.0% 0.0% 0:00 kapm-idled
4 root 19 19 0 0 0 SWN 0.0% 0.0% 0:00 ksoftirqd_CPU0
5 root 9 0 0 0 0 SW 0.0% 0.0% 0:01 kswapd
6 root 9 0 0 0 0 SW 0.0% 0.0% 0:00 kreclaimd
7 root 9 0 0 0 0 SW 0.0% 0.0% 0:00 bdflush
8 root 9 0 0 0 0 SW 0.0% 0.0% 0:01 kudpsd
```
```

The first few lines of top are most interesting, as it offers a very helpful snapshot of the current state of your system. For this particular Linux server, you can see that it's 84.6% idle (lots of CPU headroom), has 561MB of memory used and 6MB free (unsurprisingly, the kernel is maximizing the amount of physical memory it's trying to use), while 152MB of swap space is used and 177MB is free.