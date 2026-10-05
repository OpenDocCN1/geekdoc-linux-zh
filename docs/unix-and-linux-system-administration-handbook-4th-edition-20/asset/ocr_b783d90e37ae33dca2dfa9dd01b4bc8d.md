# Analyzing memory usage

memory handy that processes don't have to actually wait for a page-out each time they make a new allocation. paging increases dramatically when the system is busy, it would probably benefit from more RAM.

Linux is still evolving rapidly, and its virtual memory system has not quite finished going through puberty—it's a bit jumpy and a little bit awkward. You can tune the kernel's `swappiness` parameter (`/proc/sys/vm/swappiness`) to give the kernel a hint about how quickly it should make physical pages eligible to be reclaimed from a process in the event of a memory shortage. By default, this parameter has a value of 60. If you set it to 0, the kernel resorts to reclaiming pages that have been assigned to a process only when it has exhausted all possibilities. If you set the parameter higher than 60 (the maximum value is 100), the kernel is more likely to reclaim pages. (If you find yourself needing to modify this parameter, it's probably time to buy more RAM for the system).

If the kernel fills up RAM and swap, all VM has exhausted. Linux uses an "out-of-memory killer" to handle this condition. This function selects and a process to free memory. Although the kernel attempts to kill off the least important process on your system, running out of memory is always something to avoid. In this situation, it's likely that a substantial portion of the system's resources are devoted to memory housekeeping rather than to useful work.

# Analyzing memory usage

Two numbers summarize memory activity: the total amount of active memory and the current paging rate. The first number tells you the total demand for memory, and the second suggests the proportion of memory that is actively used. Your goal is to reduce or increase memory until paging remains at an acceptable level. Occasional paging is inevitable; don't try to eliminate it completely.

You can determine the amount of paging (swap) space that is currently in use. Run swapon -s under Solaris and AIX, and swapinfo underper HP-UX.

| swapon -s | | | Size | Used | Priority |
|---|---|---|---|---||
| /dev/hdb1 | partition | 4096532 | 0 | -1 |
| /dev/hda2 | partition | 4096564 | 0 | -2 |

| solaris$swap -l | dev swap blocks free |
|---|---|---|---||
| /dev/dsk/c0ds01 | 32,1 | 16 | 164400 | 126960 |

| hp-ux$swapinfo | | | | | | |
|---|---|---|---|---|---||
| TYPE AVAIL USED FREE USED LIMIT RESERVE PI NAME |
| dev | 3388608 | 0 | 3388608 | 0% | 0 | 1 | /dev/vg0/lv |

swapinfo and swap report usage in kilobytes, and swap -l uses 512-byte blocks. The sizes quoted by these programs do not include the contents of core memory, so you must compute the total amount of virtual memory yourself.