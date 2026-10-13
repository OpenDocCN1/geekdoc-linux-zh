
### Table A-4  *Virtual Memory*

| Parameter | Default | Category | Description/Notes |
|---|---|---|---|
| `handspreadpages` | `fastscan` | Tunable | Number of pages between the first and second scans of the page scanner. |
| `pages_before_pager` | `200` | Tunable | Used in conjunction with `lotsfree` to establish the point at which the kernel will free file system pages after an I/O. If available memory is less than `lotsfree` + `pages_before_pager`, then the kernel will free pages after an I/O (rather than keep them in the page cache for reuse). |
| `maxpgio` | `40` | Tunable | Maximum number of pageout operations per second the kernel will schedule. Set to 100 times the number of disks with swap files or swap partitions. |

## A.4  File System Parameters

The file system and page flushing parameters in Table A-5 provide for tuning file system performance and manage the flushing of dirty pages from memory to disk.

You can read more about the flush and associated parameters in “Bypassing the Page Cache with Direct I/O” on page 614. “Directory Name Cache” on page 615 and “Inode Caches” on page 617 have more information on the file system parameters, directory and inode caches.

### Table A-5  *File System and Page Flushing Parameters*

| Parameter | Default | Category | Description/Notes |
|---|---|---|---|
| `tune_t_flushr` | `5` | Tunable | `fsflush` interval; the `fsflush` daemon runs every `tune_t_flushr` seconds. |
| `autoup` | `30` | Tunable | Age in seconds of dirty pages. Used in conjunction with `tune_t_flushr`; modified pages that are older than `autoup` are written to disk. |
| `dopageflush` | `1` | Switch | When set, enables dirty page flushing by `fsflush`. Can be set to zero to disable page flushing. |
| `doiflush` | `1` | Switch | Flag to control flushing of inode cache during `fsflush` syncs. Set to 0 to disable inode cache flushing. |
| `ncsize` | `*` | Limit | Size of the directory name lookup cache (DNLC); a kernel cache that caches path names for vnodes for UFS and NFS files.<br><br>* ncsize defaults to (17 * maxusers) + 90 on 2.5.1, and (68 * maxusers) + 360 on Solaris 2.6 and 7. |
| `bufhwm` | 2% of physical memory | Limit | Maximum amount of memory (in Kbytes) allocated for the I/O buffer cache, which caches file system, indirect blocks, and directories. |
| `ndquot` | ((maxusers * 40) / 4) + max_nprocs | Limit | Number of UFS quota structures to allocate. Applies only if quotas are enabled for UFS. |
| `maxphys` | 126976 (sun4m and sun4d), 131072 (sun4u), 57344 (x86) | Limit | Maximum physical I/O size, in bytes. For some devices, the maximum physical I/O size is set dynamically when the driver loads. |
| `ufs_inode` | ncsize | Limit | Number of inodes to cache in memory. |
| `ufs:ufs_WRITES` | 1 | Switch | Enables UFS per-file write throttle. See below. |
| `ufs:ufs_LW` | 256 Kbytes | Tunable | UFS write throttle low watermark. See below. |
| `ufs:ufs_HW` | 384 Kbytes | Tunable | UFS write throttle high watermark. If the number of outstanding bytes to be written to a file exceeds `ufs_HW`, then writes are deferred until `ufs_LW` or less is pending. |
| `nrnode` | ncsize | Limit | Maximum number of inodes allocated. `nrnode` applies to NFS files, and are the NFS equivalent of a UFS inode. |
| `tmpfs_maxkmem` | Set dynamically when tmpfs is first used. | Limit | Maximum amount of kernel memory for tmpfs data structures. The value is set the first time tmpfs is used, to a range somewhere between the memory page size of the platform and 25% of the amount of available kernel memory. |
| `tmpfs_minfree` | 256 pages | Limit | Minimum amount of swap space tmpfs will leave for non-tmpfs use (i.e., the rest of the system). |

Table A-6 lists parameters related to swapfs—the pseudofile that is a key component in the management of kernel anonymous memory pages. These parameters are generally not changed from their defaults.

### Table A-6  *Swapfs Parameters*

| Parameter | Default | Category | Description/Notes |
|---|---|---|---|
| `swapfs_reserve` | 4 MB or 1/16th of memory, whichever is smaller | Limit | The amount of swap reserved for system processes. Those processes owned by root (UID 0). |
| `swapfs_minfree` | 2 MB or 1/8 of physical memory, whichever is larger | Limit | Amount of memory the kernel keeps available for the rest of the system (all processes). |

## A.5  Miscellaneous Parameters

Table A-7 lists miscellaneous kernel parameters. You can read more about many of the tunable parameters in “Kernel Bootstrap and Initialization” on page 107.

### Table A-7  *Miscellaneous Parameters*

| Parameter | Default | Category | Description/Notes |
|---|---|---|---|
| `maxusers` | MB of RAM | Limit | Generic tunable for sizing various kernel resources. |
| `ngroups_max` | 16 | Limit | Maximum number of supplementary groups a user can belong to. |
| `npty` | 48 | Limit | Number of pseudodevices, `/dev/pts` slave devices, and `/dev/pty` controller devices. |
| `pt_cnt` | 48 | Limit | Number of pseudodevices, `/dev/pts` slave devices, and `/dev/pty` master devices. |
| `rstchown` | 1 | Switch | Enables `POSIX_CHOWN_RESTRICTED` behavior. Only a root process can change file ownership. A process must be a current member of the group to which it wishes to change a file’s group, unless it is root. |
| `rlim_fd_cur` | 64 | Limit | Maximum per-process open files. |
| `rlim_fd_max` | 1024 | Limit | Per-process open files hard limit. `rlim_fd_cur` can never be larger than `rlim_fd_max`. |
| `physmem` | number of pages of RAM | Limit | Can be set to reduce the effective amount of usable physical memory. Values are in pages. |
| `kobj_map_space_len` | 1 MB | Limit | Amount of kernel memory allocated to store symbol table information. In Solaris 2.6, it defines the total space for the kernel symbol table. In Solaris 7, space is dynamically allocated as needed, in units of `kobj_map_space_len`. |
| `kmem_flags` | 0 | Switch | Solaris 2.6 and later. Enable some level of debug of kernel memory allocation. Values: 0x1 – AUDIT: maintain an activity audit log. 0x2 – TEST: Allocator tests memory prior to allocation. 0x4 – REDZONE: Allocator adds extra memory to the end of an allocated buffer, and tests to determine if the extra memory was written to when the buffer was freed. 0x8 – CONTENTS: Logs up to 256 bytes of buffer contents when buffer is freed. Requires AUDIT to also be set. |
| `kmem_debug_enable` | 0 | Switch | Kernel memory allocator debug flag. Allows kmem debug information for any or all kmem caches. Value of -1 in all caches. Solaris 2.6 and 7 only. Removed in Solaris 7, 3/99. |
| `moddebug` | 0 | Switch | Turn on kernel module debugging messages. The many possible values for moddebug can be found in `/usr/include/sys/modctl.h`. Some useful values are: 0x80000000 – print loading/unloading messages. 0x40000000 – print detailed error messages. |
| `timer_max` | 32 | Limit | Number of POSIX timers (`timer_create(2)` system call) available. |
| `consistent_coloring` | 0 | Switch | sun4u (UltraSPARC) only. Establishes the page placement policy for physical pages and L2 cache blocks. Possible values are: 0 – page coloring; 1 – virtual address = physical address; 2 – bin-hopping |

## A.6  Process and Dispatcher (Scheduler) Parameters

The parameters listed in Table A-8 relate to the process and scheduler subsystem in Solaris. For more information, refer to “The Kernel Process Table” on page 290.

### Table A-8  *Process and Dispatcher (Scheduler) Parameters*

| Parameter | Default | Category | Description/Notes |
|---|---|---|---|
| `reserved_procs` | 5 | Limit | The number of process table slots reserved for system processes. |
| `maxpid` | 30,000 | Limit | Maximum value for a PID, and the maximum number of processes that can exist on the system at any one time. |
| `max_nprocs` | (10 + 16 * maxusers) | Limit | Maximum number of processes that can exist on the system. Will be set to maxpid if it is set to a value greater than maxpid. |
| `maxuprc` | `max_nprocs - reserved_procs` | Limit | Maximum number of processes a non-root user can create. |
| `noexec_user_stack` | 0 | Switch | If set to 1, stack pages are mapped noexec, providing protection against buffer overflow attacks. 64-bit Solaris 7 maps stack pages no-exec by default. |
| `rechoose_interval` | 3 | Tunable | Clock tick count for thread-to-processor affinity scheduling. The dispatcher attempts to place a thread on the same processor it last ran on, for optimal hardware cache hits. After rechoose_interval ticks, the next available processor is chosen. |
| `hires_tick` | 0 | Tunable | Default of 0 has the system generate 100 clock interrupts per second (10 ms interval). Setting this value to 1 results in a 1 ms interval (1000 clock interrupts per second). |

## A.7  STREAMS Parameters

Table A-9 lists tunable parameters available for the kernel STREAMS subsystem. STREAMS are not covered in this version of the book.
