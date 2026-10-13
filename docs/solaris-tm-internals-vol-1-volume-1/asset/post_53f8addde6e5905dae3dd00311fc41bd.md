
name in the entry. The values in the `/etc/system` file are read at boot time, so any changes made to this file require a reboot to take effect.

These settable kernel variables are traditionally referred to as *kernel tunable parameters*. The settable kernel variables can be more accurately categorized into one of three groups:

- **Switches** — Refers to a kernel parameter that simply turns on or off a particular behavior or functional component, which, of course, affects system behavior and performance. An example of a switch is the `priority_paging` parameter, which is either on (value of 1) or off (value of 0).
- **Limits** — Refers to kernel variables that impose hard limits on a particular resource. The System V IPC tunables fall into the limit category. Several others do as well.
- **Tunables** — Refers to kernel variables that will alter performance or behavior. Think of these as a tuning knob that has a range of values (0 to *N*, where *N* represents that maximum allowable value).

Kernel parameters can be further divided into those parameters that are set on typical installations and impose minimal risk, and those that are less well known and not well understood. Changing the value of any kernel parameter imposes some level of risk. However, many of the kernel limit parameters, such as those set for System V IPC resources, are set on many installations and are generally well understood. Others can alter system behavior and performance, and sometimes it is not easy (or even possible) to predict which direction performance will move in (better or worse) as a result of changing a particular value.

In the tables that follow, we list the various kernel settable parameters, indicating their category (switch, limit, tunable) and whether or not we believe that the parameter is something that may impact system behavior in an unpredictable way, where such a warning is applicable. We also provide a reference to the page number in the book where more information about the kernel variable can be found.

> ***As a practice, you should never change a kernel settable parameter in a production system without first trying the value in a lab environment and then testing extensively.***

## A.2 System V IPC - Shared Memory Parameters

Table A-1 describes shared memory parameters. For more information, refer to “System V Shared Memory” on page 433.

### Table A-1 *System V IPC - Shared Memory*

| Parameter | Default | Category | Description / Notes |
|---|---:|---|---|
| `shmmax` | 1048576 | Limit | System V IPC shared memory. Maximum shared memory segment size, in bytes. |
| `shmmin` | 1 | Limit | System V IPC shared memory. Minimum shared memory segment size, in bytes. |
| `shmmni` | 100 | Limit | System V IPC shared memory. Maximum number of shared memory segments, systemwide. |
| `shmseg` | 6 | Limit | System V IPC shared memory. Maximum number of shared segments, per process. |
| `segspnt_minfree` | 5% of available memory | Limit | Number of pages of physical memory not available for allocation as ISM shared segments. Default value translates to allowing up to 95% of available memory get allocated to ISM shared segments. |

Table A-2 lists System V IPC semaphores. For more information, refer to “System V Semaphores” on page 444.

### Table A-2 *System V IPC - Semaphores*

| Parameter | Default | Category | Description / Notes |
|---|---:|---|---|
| `semmap` | 10 | Limit | Size of the semaphore map. |
| `semmin` | 10 | Limit | Maximum number of semaphore identifiers, systemwide. |
| `semmns` | 60 | Limit | Maximum number of semaphores, system-wide. Should be the product of `semmin` and `semmns`. |
| `semnnu` | 30 | Limit | Maximum number of semaphore undo structures, systemwide. |
| `semmsl` | 25 | Limit | Maximum number of semaphores per semaphore ID. |
| `semopm` | 10 | Limit | Maximum number of semaphore operations per `semop()` call. |
| `semume` | 10 | Limit | Maximum per-process undo structures. |
| `semvmx` | 32767 | Limit | Maximum value of a semaphore. |
| `semaem` | 16384 | Limit | Maximum adjust-on-exit value. |

Table A-3 describes message queues. For more information, refer to “System V Message Queues” on page 451.

### Table A-3 *System V IPC - Message Queues*

| Parameter | Default | Category | Description/Notes |
|---|---:|---|---|
| `msgmap` | 100 | Limit | Maximum size of resource map for messages. |
| `msgmax` | 2048 | Limit | Maximum size, in bytes, of a message. |
| `msgmnb` | 4096 | Limit | Maximum number of bytes on a message queue. |
| `msgmni` | 50 | Limit | Maximum number of message queue identifiers, systemwide. |
| `msgssz` | 8 | Limit | Message segment size. |
| `msgtql` | 40 | Limit | Maximum number of message headers, systemwide. |
| `msgseg` | 1024 | Limit | Maximum number of message segments. |

## A.3 Virtual Memory Parameters

Table A-4 lists parameters that relate to the virtual memory system and paging activity. Such activity is closely tied to file system I/O because of the buffer caching done by file systems such as UFS and VxFS.

You can read more about the memory paging parameters in “Summary of Page Scanner Parameters” on page 186, “Solaris File System Cache” on page 601, “Page Cache and Virtual Memory System” on page 605, and “In summary, we have seen a strong relationship between the VM system and file system behavior. The parameters that control the paging system have the most influence on file system performance, since they govern the way pages are made available to the file system. Figure 15.3 depicts the paging parameters that affect file systems and the memory parameters that control paging as the amount of free memory falls to the point where it hits these parameters.” on page 612.

### Table A-4 *Virtual Memory*

| Parameter | Default | Category | Description / Notes |
|---|---:|---|---|
| `fastscan` | 1/4th of physical memory, or 64 MB, whichever is larger. | Tunable | The maximum number of pages per second the page scanner will scan. |
| `slowscan` | 100 | Tunable | Initial page scan rate, in pages per second. |
| `lotsfree` | 1/64th of physical memory, or 512 KB, whichever is larger. | Tunable | Desired size of the memory free list (number of free pages). When the free list drops below `lotsfree`, the page scanner runs. |
| `desfree` | `lotsfree / 2` | Tunable | Free memory desperation threshold. When `freemem` drops below `desfree`, the page scan rate increases and the system will alter its default behavior for specific events. `desfree` must be less than `lotsfree`. |
| `minfree` | `desfree / 2` | Tunable | Minimum acceptable amount of free memory. `minfree` must be less than `desfree`. |
| `throttlefree` | `minfree` | Tunable | Memory threshold at which the kernel will block memory allocation requests. Must be less than `minfree`. |
| `pageout_reserve` | `throttlefree / 2` | Tunable | Memory pages reserved for pageout and memory scheduler threads. When `freemem` drops below `pageout_reserve`, memory allocations are denied for anything other than pageout and sched. |
| `priority_paging` | `0` | Switch | Enables priority paging when set to 1. Priority paging relieves memory pressure on executable pages due to cached file system activity. Priority paging is available for Solaris 2.6 with kernel jumbo patch 105181-10 or greater. It is in Solaris 7. |
| `cachefree` | `*` | Tunable | The memory page threshold that triggers the priority paging behavior, where file system cache pages are marked for pageout only as long as `freemem` is below `cachefree` but above `lotsfree`. `cachefree` must be greater than `lotsfree`.<br><br>* If `priority_paging` is 0, then `cachefree = lotsfree`. If `priority_paging` is 1 (enabled), then `cachefree = (lotsfree * 2)` |
| `pages_pp_maximum` | `*` | Limit | Number of pages the system requires remain unlocked.<br><br>* 200, or `tune_t_minarmem`, or 10% of available memory, whichever is greater. |
| `tune_t_minarmem` | `25` | Limit | Minimum number of memory pages reserved for the kernel. A safeguard to ensure that a minimum amount of nonswappable memory is available to the kernel. |
| `min_percent_cpu` | `4` | Tunable | Minimum percentage of CPU time pageout can consume. |
