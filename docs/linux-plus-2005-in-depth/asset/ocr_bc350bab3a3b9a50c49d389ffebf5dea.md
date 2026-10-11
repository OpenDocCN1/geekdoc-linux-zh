1726 2220 2824 3150 3232 cpuinfo kcore stat
1754 2221 2839 3151 3427 crypto kms9 swaps
1798 2232 2901 3154 347 devices loadavg sys
1804 2245 2964 3177 3576 diskstats locks sysrq-trigger
1811 2257 2978 3179 4 dma mdsstat systipc
1870 2293 2981 3181 5 dri meminfo tty
1880 2312 2983 3183 6 driver misc uptime
1915 2331 2985 3190 7 execdomains modules version
2 2347 2987 3192 8 mounts wsmaster
[root@server1 root]#

Thus, any program that can read from the /proc directory can display process information. The most common program used to display processes, aside from ps, is the **top** command and its variants. The top command displays an interactive screen listing processes organized by processor time. Processes that use the most processor time are listed at the top of the screen. An example of the screen that appears when you type the top command is shown next:

```
top - 15:02:31 up 35 min, 3 users, load average: 0.11, 0.26, 0.25
Tasks: 81 total, 2 running, 79 sleeping, 0 stopped, 0 zombie
Cpu(s): 8.4% us, 3.8% sy, 0.3% ni, 82.1% id, 5.2% wa, 0.3% hi, 0.0% si
Mem: 257100k total, 248228k used, 8880k free, 17416k buffers
Swap: 525160k total, 0k used, 525160k free, 80824k cached

 PID USER PR NI VIRT RES SHR S CPU %MEM TIME+ COMMAND
3601 root 15 0 3216 836 1620 R 3.9 0.3 0:00.02 top
2839 root 15 0 71928 24m 50m S 2.0 9.7 1:50.14 X
1 root 16 0 2028 460 1316 S 0.0 0.2 0:05.45 init
2 root 34 19 0 0 0 S 0.0 0.0 0:00.00 ksoftirqd/0
3 root 5 -10 0 0 0 S 0.0 0.0 0:00.06 events/0
4 root 5 -10 0 0 0 S 0.0 0.0 0:00.00 kblockd/0
6 root 5 -10 0 0 0 S 0.0 0.0 0:00.01 khelper
5 root 15 0 0 0 0 S 0.0 0.0 0:00.00 kthd
7 root 16 0 0 0 0 S 0.0 0.0 0:00.01 pdflush
8 root 15 0 0 0 0 S 0.0 0.0 0:00.03 pdflush
10 root 7 -10 0 0 0 S 0.0 0.0 0:00.00 aio/0
9 root 15 0 0 0 0 S 0.0 0.0 0:00.07 kswapd0
114 root 15 0 0 0 0 S 0.0 0.0 0:00.00 kseriod
153 root 15 0 0 0 0 S 0.0 0.0 0:00.12 kjournald
347 root 6 -10 1736 288 1228 S 0.0 0.1 0:00.02 udevd
1681 root 16 0 2396 624 1296 S 0.0 0.2 0:00.07 syslogd
1685 root 16 0 3024 440 1244 S 0.0 0.2 0:00.01 klogd
1706 rpc 16 0 1656 580 1372 S 0.0 0.2 0:00.00 portmap
1726 rpcuser 23 0 2604 724 1380 S 0.0 0.3 0:00.00 rpc.statd
```