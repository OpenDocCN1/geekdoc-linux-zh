The top program displays a continuously updating (by default, every 3 seconds) display of the system processes listed in order of process activity. The name "top" comes from the fact that the top program is used to see the "top" processes on the system. The top display consists of two parts: a system summary at the top of the display, followed by a table of processes sorted by CPU activity:

```
top - 14:59:20 up 6:30, 2 users, load average: 0.07, 0.02, 0.00
Tasks: 109 total, 1 running, 106 sleeping, 0 stopped, 2 zombie
Cpu(s): 0.7%us, 1.0%sy, 0.0%ni, 98.3%id, 0.0%wa, 0.0%hi, 0.0%si
Mem: 319496k total, 314860k used, 4636k free, 19392k buff
Swap: 875500k total, 149128k used, 726372k free, 114676k cach

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
6244 me 39 19 31752 3124 2188 R 6.3 1.0 16:24.42 tracker d
11071 me 20 0 2304 1092 840 R 1.3 0.3 0:00.14 top
6180 me 20 0 2700 1100 772 S 0.7 0.3 0:03.66 dbus-da e
6321 me 20 0 20944 7248 6560 S 0.7 2.3 2:51.38 multiload
4955 root 20 0 104m 9668 5776 S 0.3 3.0 2:19.39 Xorg
1 root 20 0 2976 528 476 S 0.0 0.2 0:03.14 init
2 root 15 -5 0 0 0 S 0.0 0.0 0:00.00 kthreadd
3 root RT -5 0 0 0 S 0.0 0.0 0:00.00 migratio
4 root 15 -5 0 0 0 S 0.0 0.0 0:00.72 ksoftirq
5 root RT -5 0 0 0 S 0.0 0.0 0:00.04 watchdog
6 root 15 -5 0 0 0 S 0.0 0.0 0:00.42 events/0
7 root 15 -5 0 0 0 S 0.0 0.0 0:00.06 khelper
41 root 15 -5 0 0 0 S 0.0 0.0 0:01.08 kblockd/
67 root 15 -5 0 0 0 S 0.0 0.0 0:00.00 kseriod
114 root 20 0 0 0 0 S 0.0 0.0 0:01.62 pdflush
116 root 15 -5 0 0 0 S 0.0 0.0 0:02.44 kswapd0
```

The system summary contains a lot of good stuff. Here's a rundown:

# Table 11-3: top Information Fields

| Row | Field | Meaning |
|---|---|---|
| 1 | top | Name of the program. |
|  | 14:59:20 | Current time of day. |
|  | up 6:30 | This is called uptime. It is the amount of time since the machine was last booted. In this example, the system has been up for six and a half hours. |
|  | 2 users | There are two users logged in. |
|  | load average: | Load average refers to the number of processes |