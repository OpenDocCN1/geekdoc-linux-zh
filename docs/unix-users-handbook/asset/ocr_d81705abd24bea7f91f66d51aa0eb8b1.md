```
c0t1d0    0
c0t3d0    0
c0t5d0    0

VM
    memory
    avm free re at pl page fr de sr in faults
    1219  425  0  0   0   0  0  0  0  111   54  15

    CPU
    us sy id r b w
    1  8  92  0  0   0

Disk Transfers
device    xfer/sec
c0t6d0    0
c0t1d0    0
c0t3d0    0
c0t5d0    0
```

+   8. Display the number of forks and pages of virtual memory since boot-up.

```
vmstat -f

24558 forks, 1471595 pages, average= 59.92
```

+   9. Display the counts of paging-related events.

```
vmstat -s

0 swap ins
0 swap outs
0 pages swapped in
0 pages swapped out
1344563 total address trans. faults taken
542093 page ins
2185 page outs
602573 pages paged in
4346 pages paged out
482343 reclaimss from free list
504621 total page reclaims
124 intransit blocking page faults
1460755 zero fill pages created
404137 zero fill page faults
366022 executable fill pages created
71578 executable fill page faults
0 swap text pages found in free list
162043 incode text pages found in free list
196 revolutions of the clock hand
45732 pages scanned for page out
4859 pages freed by the clock daemon
36680636 cpu context switches
1497746186 device interrupts
1835626 traps
87434493 system calls
```

WARNINGS

Users of vmstat must not rely on the exact field widths and spacing of its output, as these will vary depending on the system, the release of HP-UX, and the data to be displayed.

AUTHOR

vmstat was developed by the University of California, Berkeley and HP.