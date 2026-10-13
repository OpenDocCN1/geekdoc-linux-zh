
Also, you can use the `modload(1M)` command, which allows a root user to load any loadable kernel module from the command line. You can use the `modinfo(1M)` command to see which loadable modules are currently loaded in the kernel. Note that Solaris is smart enough not to allow the unloading (`modunload(1M)`) of a loadable module that is in use. Note also that the code is written to be aware of dependencies, such that loading the `shmsys` module also causes the `ipc` module to be loaded.

The kernel maintains certain resources for the implementation of shared memory. Specifically, a shared memory identifier, `shmid`, is initialized and maintained by the operating system whenever a `shmget(2)` system call is executed successfully. The `shmid` identifies a shared memory segment that has two components: the actual shared RAM pages and a data structure that maintains information about the shared segment, the `shmid_ds` data structure, detailed in Table 10-4.

**Table 10-4** *shmid_ds Data Structure*

| Name | Data Type | Corresponding ipcs(1M) Column | Description |
|---|---|---|---|
| `shm_perm` | struct | see ipc perm table | Embedded `ipc_perm` structure. Generic structure for IPC facilities that maintains permission information |
| `shm_segsz` | unsigned int | SEGSZ | Size in bytes of the shared segment |
| `shm_amp` | pointer | none | Pointer to corresponding anon map structure |
| `shm_lkcnt` | unsigned short | none | Lock count—number of locks on the shared segment |
| `shm_lpid` | long | LPID | Last PID; PID of last process to do a shared memory operation on the segment |
| `shm_cpid` | long | CPID | Creator PID; PID of the process that created the shared segment |
| `shm_nattch` | unsigned long | NATTCH | Number of attaches to the shared segment |
| `shm_cnattch` | unsigned | none | Creator attaches? *Not currently used* |
| `shm_atime` | long | ATIME | Time of last attach |
| `shm_dtime` | long | DTIME | Time of last detach |
| `shm_ctime` | long | CTIME | Time of last change to shmid_ds structure |
| `shm_cv` | cond var | none | Condition variable. *Not used* |
| `shm_sptas` | pointer | none | Pointer to address space structure |

The system allocates kernel memory for some number of `shmid_ds` structures at boot time, as determined from the shared memory tunable parameter `shmmni`. All together, only four tunable parameters are associated with shared memory. They are described in Table 10-5.

**Table 10-5** — *Shared Memory Tunable Parameters*

| Name | Default Value | Minimum Value | Maximum Value | Data Type | Description |
|---|---:|---:|---:|---|---|
| `shmmax` | 1048576 | 1 | 4,294,967,295 (4 GB) | unsigned int | Maximum size in bytes of a shared memory segment |
| `shmmin` | 1 | 1 | 4,294,967,295 (4 GB) | unsigned int | Minimum size for a shared segment |
| `shmmni` | 100 | 1 | 2147483648 (2 GB) | int | Maximum number of `shmid_ds` structures, systemwide. |
| `shmseg` | 6 | 1 | 32767 (32K) | short | Max segments per process |

When the system first loads the shared memory module, it allocates kernel memory to support the `shmid_ds` structures and other required kernel support structures. Each `shmid_ds` structure is 112 bytes in size and has a corresponding kernel mutex lock, which is an additional 8 bytes. Thus, the amount of kernel memory required by the system to support shared memory can be calculated as ((`shmmni` * 112) + (`shmmni` * 8)). The default value of 100 for `shmmni` requires the system to allocate 112.8 Kbytes of kernel memory for shared memory support. The system makes some attempt to protect itself against allocating too much kernel memory for shared memory support by checking for the maximum available kernel memory, dividing that value by 4, and using the resulting value as a limit for allocating resources for shared memory. Simply put, the system will not allow more than 25 percent of available kernel memory to be allocated.

The preceding description applies to Solaris 2.5, 2.5.1, and 2.6. Prior releases, up to and including Solaris 2.4, did not impose a 25 percent limit check. Nor did they require the additional 8 bytes per `shmid_ds` for a kernel mutex lock, since shared memory used very coarse grained locking in the earlier releases and only implemented one kernel mutex in the shared memory code. Beginning in Solaris 2.5, finer-grained locking was implemented, allowing for greater potential parallelism of applications using shared memory.

It should be clear that one should not set `shmmni` to an arbitrarily large value simply to ensure sufficient resources. There are limits as to how much kernel memory the system supports. On sun4m-based platforms, the limits are on the order of 128 Mbytes for releases prior to Solaris 2.5, and 256 Mbytes for Solaris 2.5, 2.5.1, and 2.6. On sun4d systems (SS1000 and SC2000), the limits are about 576 Mbytes in Solaris 2.5 and later. On UltraSPARC-based (sun4u) systems, the kernel has its own 4-Gbyte address space, so it is much less constrained. Still, keep in mind that the kernel is not pageable, and thus whatever kernel memory is needed remains resident in RAM, reducing available memory for user processes. Given that Sun ships systems today with very large RAM capacities, this characteristic of the kernel may not be an issue, but it should be considered nonetheless.

Note that the maximum value for `shmmni` listed in Table 10-5 is 2 Gbytes. This is a theoretical limit, based on the data type (a signed integer), and should not be construed as something configurable today. Applying the math from above, you see that 2 billion shared memory identifiers would require over 200 Gbytes of kernel memory! Assess to the best of your ability the number of shared memory identifiers required by the application, and set `shmmni` to that value plus 10 percent or so for headroom.

The remaining three shared memory tunable parameters are defined quite simply.

`shmmax` defines the maximum size a shared segment can be. The size of a shared memory segment is determined by the second argument to the `shmget(2)` system call. When the call is executed, the kernel checks to ensure that the size argument is not greater than `shmmax`. If it is, an error is returned. Setting `shmmax` to its maximum value does not affect the kernel size—no kernel resources are allocated on the basis of `shmmax`, so this variable can be tuned to its maximum value of 4 Gbytes (0xffffffff) on a 32-bit Solaris system, and larger on a 64-bit Solaris 7 system. The /etc/system entry examples that follow illustrate two ways of setting the 4-Gbyte limit for a 32-bit system and setting something larger on a 64-bit Solaris 7 system, in this case, a 10-Gbyte maximum shared segment.

```text
set shmsys:shminfo_shmmax=0xffffffff       /* hexadecimal - 4GB limit */
set shmsys:shminfo_shmmax=4294967295       /* decimal - 4GB limit */
set shmsys:shminfo_shmmax=10000000000      /* decimal - 10GB, 64-bit example */
```

The `shmmin` tunable defines the smallest possible size a shared segment can be, as per the size argument passed in the `shmget(2)` call. There’s no compelling reason to set this tunable from the default value of 1.

Lastly, `shmseg` defines the number of shared segments a process can attach (map pages) to. Processes can attach to multiple shared memory segments for application purposes, and this tunable determines how many mapped shared segments a process can have attached at any one time. Again, the 32-Kbyte limit (maximum size) in Table 10-5 is based on the data type (short) and does not necessarily reflect a value that will provide application performance that meets business requirements if some number of processes attach to 32,000 shared memory segments. Things like shared segment size, system size (amount of RAM, number and speed of processors, etc.) all factor in determining the extent to which you can push the boundaries of this facility.

### 10.2.1 Shared Memory Kernel Implementation

In this section we look at the flow of kernel code that executes when the shared memory system calls are called.

Applications first call `shmget(2)` to get a shared memory identifier. The kernel uses a key value passed in the call to locate (or create) a shared segment.

```text
[application code]
shmget(key, size, flags [PRIVATE or CREATE])

[kernel]
shmget()
        ipcget() /* get an identifier - shmid_ds */
        if (new shared segment)
                check size against min and max tables
                get anon_map and anon array structures
                initialize anon structures
                initialize shmid_ds structure
        else /* existing segment */
                check size against existing segment size
        return shmid (or error) back to application
ipcget()
        if (key == IPC_PRIVATE)
                loop through shmid_ds structures, looking for a free one
                        if (found)
                                goto init
                        else
                                return ENOSPC /* tough cookies */
        else /* key is NOT IPC_PRIVATE */
                loop through shmid_ds structures, for each one
                        if (structure is allocated)
                                check if the key matches
                                if (CREATE or EXCLUSIVE flags set as passed args)
                                        return EEXIST or error /* segment with matching key exists */
                                if (permissions do NOT allow access)
                                        return EACCES
                                set status
                                set base address of shmid_ds
                                return 0 /* that's a good thing */

        set base address of shmid_ds /* if we reach this, we have an unallocated shmid_ds structure */
                if (do not CREATE)
                        return ENOENT error /* we're through them all, and didn't match keys */
                if (CREATE and no space)
                        return ENOSPC error
                do init
                return 0 /* goodness */
```

`shmget()`, when entered, calls `ipcget()` to fetch the `shmid_ds` data structure. Remember, all possible `shmid_ds` structures are allocated up-front when `/kernel/sys/shmsys` loads, so we need to either find an existing one that matches the key value or initialize an unallocated one if the flags indicate we should and a structure is available. The final init phase of `ipcget()` sets the mode bits, creator UID, and creator GID. When `ipcget()` returns to `shmget()`, the anon page mappings are initialized for a new segment or a simple size check is done. (The size
