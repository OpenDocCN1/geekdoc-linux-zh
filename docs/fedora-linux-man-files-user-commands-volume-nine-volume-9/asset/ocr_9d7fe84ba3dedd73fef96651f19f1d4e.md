support has been included.

| **lwp** | LWP | light weight process (thread) ID of the dispatchable entity (alias `spid`, `tid`). See **`tid`** for additional information. |
|---|---|---|
| **machine** | MACHINE | displays the machine na for processes assigned to VM or container, if systemd support has been included. |
| **maj\_flt** | MAJFLT | The nuer of major page faults that have occurred with this process. |
| **min\_flt** | MINFLT | The nuer of minor page faults that have occurred with this process. |
| **mntns** | MNTNS | Unique inode nuer describing the namespace the process belongs to. See `(7)`. |
| **netns** | NETNS | Unique inode nuer describing the namespace the process belongs to. See `(7)`. |
| **ni** | NI | nice value. This ranges from 19 (nicest) to -20 (not nice to others), see `(1)`. (alias **`nice`**). |
| **nice** | NI | see **`ni`**.(alias **`ni`**). |
| **nlwp** | NLWP | nuer of lwps (threads) in the process. (alias **`thcount`**). |
| **nwchan** | WCHAN | address of the kernel function where the process is sleeping (use **`wchan`** if you want the kernel function na). Running tasks will display a dash (`-`) in this column. |
| **ouid** | OWNER | displays the Unix user identifier of the owner of the session of a process, if systemd support has been included. |
| **pcpu** | %CPU | see **`%cpu`**. (alias **`%cpu`**). |
| **pending** | PENDING | mask of the pending signals. See `(7)`. Signals pending on the process are distinct from signals pending on individual threads. Use the `m` option or the `-m` option to see both. According to the width of the field, a 32 or 64 bits mask in hexadecimal format is displayed. (alias **`sig`**). |
| **pgid** | PGID | process group ID or, equivalently, the process ID of the process group leader. (alias **`pgrp`**). |
| **pgrp** | PGRP | see **`pgid`**. (alias **`pgid`**). |
| **pid** | PID | a nuer representing the process ID (alias **`tgid`**). |
| **pidns** | PIDNS | Unique inode nuer describing the namespace the process belongs to. See `(7)`. |
| **pm** | %MEM | see **`%m`**. (alias **`%m`**). |
| **policy** | POL | scheduling class of the process. (alias **`class`**, **`cls`**). Possible values are:
`-not` `reported` `TSSCHED_OTHER` `FSSCHED_FIFO` `RRSCHED_RR` `BSCHED_BATCH` `IOSCHED_ISO` |