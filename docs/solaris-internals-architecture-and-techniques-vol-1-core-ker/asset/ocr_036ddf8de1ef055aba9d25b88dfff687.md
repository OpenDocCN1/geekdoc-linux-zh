# Table 10-6 Semaphore Kernel Tunables

| Name | Default Value | Maximum Value | Data Type | Description |
| --- | --- | --- | --- | --- |
| semmap | 10 | 2 billion | signed int | Size of semaphore resource map |
| semmni | 10 | 65536 | signed int | Number of semaphore identifiers |
| semmnns | 60 | 2 billion | signed int | Total semaphores, system-wide |
| semmnu | 30 | 2 billion | signed int | Total undo structures, system-wide |
| semmsl | 25 | 65536 | unsigned short | Maximum number of semaphores per identifier |
| semopm | 10 | 2 billion | signed int | Maximum operations per semop(2) call |
| semume | 10 | 2 billion | signed int | Maximum entries per process |
| semusz | 96 | 2 billion | signed int | Total bytes required for undo structures, system-wide |
| semvmx | 32767 | 65536 | unsigned short | Maximum value of a semaphore |
| semaem | 16384 | 32767 | signed short | Maximum adjust on exit value |

+   **semmap** - Determines the maximum number of entries in a semaphore map. The memory space given to the creation of semaphores is taken from the value of `semmap`. The implementation of allocation maps is generic within UNIX SVR4 and Solaris, supported by a standard set of kernel routines (`rmalloc()`, `rmfree()`, etc.).
The use of allocation maps by the semaphore subsystem is one example of their implementation. They basically prevent the kernel from having to deal with allocation and deallocating kernel memory as semaphores are initialized and freed. Initialization and use of allocation maps, kernel memory is allocated up-front, and map entries are allocated and freed dynamically from the semaphore allocation maps. Given that `semmns` limits the total number of semaphores systemwide and that semaphore is also allocated from the resource map, it makes sense to set `semmap` equal to `semmns`.
**semmni** - Establishes the maximum number of systemwide semaphore sets. Every semaphore set in the system has a unique identifier and control structure, the `semid_ds` data structure. During init, the system allocates kernel