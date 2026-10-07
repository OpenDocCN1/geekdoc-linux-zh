
# Table 7-6 MemTool Buffer Cache Fields

| Field | Description |
| --- | --- |
| Resident | The amount of physical memory that this file has associated with it. |
| Used | The amount of physical memory that this file has mapped into a process segment or SEMAP. Generally, the difference between this and the resident figure is what is on the free list associated with this file. |
| Shared | The amount of memory that this file has in memory that is shared with more than one process. |
| Pageins | The amount of minor and major page-ins for this file. |
| Pageouts | The amount of page-outs for this file. |
| Filename | The filename if known; otherwise, the file system mount point and inode number are shown. |

## 7.4.3.2 Process Memory

The second mode of the MemTool GUI is the process memory display. Click on the Process Memory checkbox at the left of the GUI to select this mode. The process memory display shows the process table with a memory summary for each process. Each line of the process table is the same as the per-process summary from the pmap command. Figure 7.3 shows the fields; Table 7-7 describes them.

# Bunyip Memory Tool

File Options

| Display Type | | Show | Selection Totals |
|---|---|---|---|---|---|
| ☐ VFS Memory | Processes | 144 | All/Filter | Private | Ok |
| ☑ Process Memory | out of | 144 | Selected | Text/Library | Ok |
| ☐ Process Matrix | Files | 0 | Filters | Total | Ok |

| PID | Virtual | Resident | Shared | Private | Process Name |
|---|---|---|---|---|---|
| 434 | 185096k | 28782k | 1256k | 26616k | /usr/openwin/bin/xsun -dev /dev/fs/ |
| 26734 | 94132k | 22846k | 18368k | | /usr/bin/dmtail |
| 683 | 28016k | 17047k | 8056k | /usr/dist/share/framemaker,V.1/bin/ |
| 17954 | 17664k | 9664k | 5112k | 4552k | /usr/bin/dmtail -session dfsRh/ |
| 26731 | 8352k | 6056k | 3520k | 3136k | /netscape |
| 1951 | | | | | /usr/sbin. |

| PID | Adr. | Size | Res | Shared | Prt | Segment-Name |
|---|---|---|---|---|---|---|
| 25851 | 0001000 | 36k | Ok | Ok | read/write/exec | /8000728:2026/9 |
| 6140 | 00037000 | 40k | Ok | Ok | read/write/exec | |
| 738 | 00038000 | 58k | Ok | Ok | read/write/exec | |
| 1795 | EE420000 | | | Ok | Ok | read/write/exec | |
| 2367 | EE600000 | | Ok | Ok | read/write/exec | |
| 544 | EE620000 | | Ok | Ok | read/write/exec | |
| 266 | EE6C0000 | | Ok | Ok | read/write/exec | |
| 529 | EE813000 | | Ok | Ok | read/write/exec | |
| 17163 | EEE10000 | | Ok | Ok | read/write/exec | /8000728:1116 |
| 290 | EEE20000 | 16k | Ok | Ok | read/write/exec | /8000728:1116 |
| 557 | EEE30000 | | Ok | Ok | read/write/exec | /8000728:1116 |
| 553 | EEE40000 | | Ok | Ok | read/write/exec | server |
| 613 | EEE50000 | | Ok | Ok | read/write/exec | server |
| 1034 | EEE60000 | | Ok | Ok | read/write/exec | comeuro.so.2 |
| 558 | EEE70000 | | Ok | Ok | read/write/exec | xkind.so.2 |
| 562 | EE770000 | | Ok | Ok | read/write/exec | xlib118n.so.2 |
| 560 | EE771000 | | Ok | Ok | read/write/exec | ZkRe- |
| 559 | | | | | | p 8157- |

Figure 7.3 MemTool GUI: Process Field

Table 7-7 MemTool Process Table Field

| Field | Description |
|---|---|
| PID | Process ID of the process |
| Virtual | The virtual size of the process, including swapped-out and unallocated memory. |
| Resident | The amount of physical memory that this process has, including shared binaries, libraries, etc. |

# Table 7-7 MemTool Process Table Field (Continued)

| Field | Description |
| --- | --- |
| Shared | The amount of memory that this process is sharing with another process, that is, shared libraries, shared memory, etc. |
| Private | The amount of resident memory this process has that is not shared with other processes. This figure is essentially—Resident—Shared. |
| Process | The full process name and arguments. |

To select the individual process map for a process, click on one of the process entries.

## 7.4.3.3 Process Matrix

The process matrix, Figure 7.4, shows the relationship between processes and mapped files. Across the top of the display is the list of processes we viewed in these processes memory, and down the side is a list of the files that are mapped into these processes. Each column of the matrix shows the amount of memory mapped into that process for each file, with an extra row for the private memory associated with that process. The matrix can be used to show the total memory usage of a group of processes. By default, the summary box at the top right-hand corner shows the memory used by all processes. We can select a group of processes with the left button and then summarize by pressing the button at the top-middle of the display. Selecting the All/Filter button returns the full display.

## 7.5 Memory Monitoring

![](img/a86367b95bf21add858c9948ac951c6_295_0.png)

Figure 7.4 MemTool GUI: Memory/File



7.5 Other Tools

Two other tools—Workspace Monitor (wsm) and memstat (vmstat)—provide additional information.

7.5.1 The Workspace Monitor: WSM

Another good utility for memory usage is the workspace monitor. It shows a live status of a process's memory map and lists the amount of memory that has been written or read in the sampled interval. This information is particularly useful for determining how much memory a process is using at any given instant. The wsm command is invoked against a single process.

```
wsm -p 732 -t
Read Mapped PROT Segment.exe (pid 683) Mon 21 15:44
235 0 782 (R)
10 11 36 (RWX)
207 384 2690 (RWX) /usr/lib/libc.so
14 0 74 (R) /usr/lib/libc.so
2 2 (1) /dev/zero (or other device)
0 0 1 (R) /stradd.so
0 0 1 (RWX) /str.so
1 0 2 (R) /platform/psr.so
0 0 1 (RWX) /dev/zero (or other device)
0 0 56 (RWX) /usr/libsm1.so
0 0 4 (RWX) /usr/libsm1.so
0 0 2 (R) /dev/zero (or other device)
0 0 2 (R) /usr/libmsp.so
0 0 9 (RWX) /usr/libmsp.so
0 0 9 (RWX) /usr/openwin/libext.so
26 0 54 (R) /usr/openwin/lib11.so
0 2 3 (RX) /usr/openwin/lib11.so
0 0 4 (RWX) /usr/libsocket.so
0 0 1 (RWX) /dev/zero (or other device)
0 0 1 (R) /usr/libd.so
0 0 14 (RWX) /usr/libd.so
2 0 2 (RWX) /usr/libd.so
500 401 3753 (RWX) totals
```

The counters in the wsm utility are in units of pages: the Solaris kernel. Later, in Solaris 8, a new vmstat option (-p) was added to examine these statistics. The statistics can be observed on Solaris 7 with a simple command-line utility: memstat. memstat shows the paging activity, page-ins, page-outs, and page-frees separated into three classes: file system paging, anonymous memory paging, and executable/shared library paging.

## 7.5.2 An extended vmstat Command: memstat

free = free memory measured in pages

### Global Page Counters
- re = pages reclaimed from the free list
- mf = minor faults - the page was in memory but not mapped
- pi = pages paged in from file system or swap device
- po = pages paged out to file system or swap device
- de = pages that have been destroyed or freed

### Executable Page Counters
- epi = executable and library pages that are paged in
- epo = executable and library pages that are paged out (should be zero)
- epf = executable and library pages that are freed

### CPU Summary
- us = user cpu time
- sky = kernel cpu time
- wt = wait cpu time
- d = idle cpu time

### Anonymous Page Counters
- api = anonymous pages that are paged in swap
- apo = anonymous pages that are paged out swap
- pf = anonymous pages that are freed

### File Page Counters
- api = file pages that are paged in
- apo = file pages that are paged out
- pf = file pages that are freed

![](img/a86367b95bf21add858c9948ac951c6_297_0.png)

| memory free re mf pi po fr de re epi epo epf apo fpi fpo wpo us ky wt id |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 16128 | 8 | 0 | 341 | 1629 | 1677 | 0 | 0 | 0 | 0 | 0 | 0 | 85 | 88 | 341 | 1629 | 1677 | 45 | 34 | 27 |
| 15184 | 12 | 0 | 350 | 1720 | 2434 | 0 | 437 | 0 | 0 | 2 | 0 | 85 | 81 11 | 1634 | 2334 | 19 | 35 | 43 |
| 15152 | 6 | 0 | 160 | 1520 | 2541 | 0 | 490 | 0 | 0 | 0 | 16 | 85 | 114 | 1605 | 1430 | 241 | 22 | 40 |
| 14968 | 19 | 0 | 162 | 1688 | 3285 | 0 | 698 | 0 | 0 | 68 | 181 | 1622 | 1520 | 385 | 21 | 29 | 34 |
| 15386 | 23 | 19 | 242 | 2332 | 3573 | 0 | 595 | 0 | 06 | 12 | 149 | 204 | 2119 | 273 | 27 | 32 | 35 |
| 15704 | 8 | 0 | 194 | 2102 | 3960 | 0 | 0 | 0 | 0 | 0 | 200 | 394 | 581 | 11 | 41 | 46 | 38 |
| 16192 | 16 | 5 | 202 | 1889 | 1900 | 0 | 0 | 0 | 0 | 0 | 200 | 202 | 189 | 11 | 41 | 47 | 44 |
| 16976 | 4 | 54 | 200 | 40 | 40 | 0 | 0 | 0 | 0 | 0 | 200 | 40 | 1 | 16 | 37 | 46 | |
| 17376 | 1 | 8 | 194 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 194 | 40 | 2 | 14 | 39 | 44 | |

The columns for the memstat command are described in Table 7-8.

| Counter | Description |
|---|---|
| free | The amount of free memory as reported by vmstat, which reports the bins size of the cache and free list. memory on Solaris 7 may contain some of the file system cache |
