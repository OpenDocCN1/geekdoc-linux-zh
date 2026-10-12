A sample syntax with an interval of five seconds and five counts would look like this:

```
$ vmstat 5 5
procs memory swap io system cpu
r b w swap free buff cache si so bi bo in cs us sy id
1 0 0 68 5416 2724 25796 0 0 1 0 113 57 1 0 99
0 0 0 68 5424 2724 25796 0 0 0 2 108 28 1 0 99
0 0 0 68 5424 2724 25796 0 0 0 1 106 25 0 1 99
0 0 0 68 5424 2724 25796 0 0 0 0 105 25 0 1 99
0 0 0 68 5424 2724 25796 0 0 0 0 102 25 0 0 99
```

The very first line output by vmstat is the average values for statistic since boot time (so don't be alarmed).

vmstat is actually broken up into five sections: procs, memory, swap, io, and cpu.

Each section is outlined in the following tables.

The procs section:

| Procs | Description |
|---|---|
| r | Number of processes waiting for run time |
| b | Number of interrupted sleep processes |
| w | Number of swapped out processes, but able to run |

The memory section:

| Memory | Description |
|---|---|
| Swpd | Amount of virtual memory used in kbytes |
| Free | Amount of idle memory used in kbytes |
| Buff | Amount of memory used by buffers in kbytes |
| Cache | Amount of memory left in cache in kbytes |

The swap section:

| Swap | Description |
|---|---|
| si | Amount of memory swapped in from disk in kbytes |
| so | Amount of memory swapped to disk |