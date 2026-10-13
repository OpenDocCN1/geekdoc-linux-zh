# 10.2.1 Shared Memory Kernel Implementation

In this section we look at the flow of kernel code that executes when the shared memory system calls are called.

Applications first call shmget(2), to get a shared memory identifier. The kernel uses a key value passed in the call to locate (or create) a shared segment.

```
```text
[application code]
shmget(key, size, flags [PRIVATE or CREATE])

[kernel]
shmget()
        ipcg et() /* get an identifier - shmid_ds */
        if (new shared segment)
                check size against min and max tables
                get anon_map and anon array structures
                initialize anon structures
                initialize shmid_ds structure
        else /* existing segment */
                check size against existing segment size
        return shmid (or error) back to application
ip cget()
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
```

shmget(), when entered, calls ipcget() to fetch the shmid_ds data structure. Remember, all possible shmid_ds structures are allocated up-front when /kernel/sys/shmsys loads, so we need to either find an existing one that matches the key value or initialize an unallocated one if the flags indicate we should and a structure is available. The final init phase of ipcget() sets the mode bits, creator UID, and creator GID. When ipcget() returns to shmget(), the anon page mappings are initialized for a new segment or a simple size check is done. (The size