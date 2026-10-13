# **Table 10–6** *Semaphore Kernel Tunables (Continued)*

| Name | Default Value | Maximum Value | Data Type | Description |
|---|---:|---:|---|---|
| `semmnu` | 30 | 2 billion | signed int | Total undo structures, systemwide |
| `semmsl` | 25 | 65536 | unsigned short | Maximum number semaphores per identifier |
| `semopm` | 10 | 2 billion | signed int | Maximum operations per `semop(2)` call |
| `semume` | 10 | 2 billion | signed int | Maximum undo entries per process |
| `semusz` | 96 | 2 billion | signed int | Total bytes required for undo structures, systemwide |
| `semvmx` | 32767 | 65536 | unsigned short | Maximum value of a semaphore |
| `semaem` | 16384 | 32767 | signed short | Maximum adjust on exit value |

+   - **semmap** — Determines the maximum number of entries in a semaphore map. The memory space given to the creation of semaphores is taken from the semmap, which is initialized with the number of map entries fixed by the value of semmap. The implementation of allocation maps is generic within UNIX SVR4 and Solaris, supported with a standard set of kernel routines (`rmalloc()`, `rmfree()`, etc.).
+   
+     The use of allocation maps by the semaphore subsystem is just one example of their implementation. They basically prevent the kernel from having to deal with allocating and deallocating additional kernel memory as semaphores are initialized and freed. By initialization and use of allocation maps, kernel memory is allocated up-front, and map entries are allocated and freed dynamically from the semmap allocation maps. Given that semmns limits the total number of semaphores systemwide and that semaphore space is allocated from the resource map, it makes sense to set semmap equal to semmns.

+   - **semnni** — Establishes the maximum number of systemwide semaphore sets. Every semaphore set in the system has a unique identifier and control structure, the semid_ds data structure. During init, the system allocates kernel memory for semid_ds control structures as determined from the semmni tunable. Each control structure is 84 bytes, so as with the shared memory shmnni tunable, you should avoid making this value arbitrarily large.

+   - **semmns** — Defines the maximum number of semaphores in the system. A semaphore set can have more than one semaphore associated with it, and each semaphore has a corresponding sem data structure. Each sem structure is only 16 bytes, but you still shouldn’t go over the edge with this (do not