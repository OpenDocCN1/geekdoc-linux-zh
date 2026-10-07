# Bunyip Memory Tool

File Options

| Display Type | | Show | Selection Totals |
|---|---|---|---|---||
| ☐ VFS Memory | Processes | 144 | All/Filter | Private | Ok |
| ☑ Process Memory | out of | 144 | Selected | Text/Library | Ok |
| ☐ Process Matrix | Files | 0 | Filters | Total | Ok |

| PID | Virtual | Resident | Shared | Private | Process Name |
|---|---|---|---|---|---|n| 434 | 185096k | 28782k | 1256k | 26616k | /usr/openwin/bin/xsun -dev /dev/fs///
| 26734 | 94132k | 22846k | 18368k | | /usr/bin/dmtail |
| 683 | 28016k | 17047k | 8056k | /usr/dist/share/framemaker,V.1/bin///
| 17954 | 17664k | 9664k | 5112k | 4552k | /usr/bin/dmtail -session dfsRh///
| 26731 | 8352k | 6056k | 3520k | 3136k | /netscape |
| 1951 | | | | | | /usr/sbin. |

| PID | Adr. | Size | Res | Shared | Prt | Segment-Name |
|---|---|---|---|---|---|---|n| 25851 | 0001000 | 36k | Ok | Ok | read/write/exec | /8000728:2026/9 |
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
| 559 | | | | | | | p 8157- |

Figure 7.3 MemTool GUI: Process Field

Table 7-7 MemTool Process Table Field

| Field | Description |
|---|---|n| PID | Process ID of the process |
| Virtual | The virtual size of the process, including swapped-out and unallocated memory. |
| Resident | The amount of physical memory that this process has, including shared binaries, libraries, etc. |