
# Analyzing CPU usage

The second CPU statistic's useful for characterizing the burden on your system is the "load average," which represents the average number of runnable processes. It gives you a good idea of how many pieces the CPU pie is divided into. The load average is obtained with the uptime command:

```

$ uptime
```

11:10am up 34 days, 18:42, 5 users, load average: 0.95, 0.38, 0.31

Three values are given, corresponding to the 5, 10, and 15-minute averages. In general, the higher load average, the more important the system's aggregate performance becomes. If there is only one runnable process, that process is usually bound by a single resource (commonly disk bandwidth or CPU). The demand for one resource becomes the determining factor in performance.

When more processes share the system, loads may or not be even more distributed. If the processes on the system consume a mixture of CPU, disk, and memory, the performance of the system is less likely to be dominated by constraints on a single resource. In this situation, it becomes important to look at measures of consumption, such as CPU utilization.

Modern single-processor systems are typically busy with a load average of 3 and not deal well with load averages over 0.8. A load average of this magnitude is a hint that you should look for ways to spread the load artificially, by using nice to set process priorities.

See page 123 for more information.

The load average is an excellent metric to track as part of a system-baseline. If you monitor your system's load average on a normal day and it is in that same range on a bad day, this is a hint that you should look elsewhere (such as the network) for performance problems. A load average above the expected norm suggests that you should look at the processes running on the system.

Another way to view CPU usage is to run the ps command with arguments that show how much of the CPU each process is using (-aux for Linux and AIX -elf for HP-UX and Solaris). On a busy system, at least 70% of the CPU is consumed by one or two processes. Deferring the execution of the CPU hogs reducing their priority makes the CPU more available to others.

An alternative to ps is program called top. It presents about the same information as ps, but in live, regularly updated format that shows the status of the system over time. AIX's top command is even nicer.

See page 133 for more information.

On virtualized systems, ps, top, and other command display CPU utilization may be misleading. A virtual machine that is not using all of its CPU cycles allows other virtual machines to we (steal) those cycles. Any measurement that is relative to the operating system, as clock ticks per second, should be examined carefully to be sure what is actually being reported.

Refreshing top's output too rapidly can itself be a CPU hog, so be be judicious in your use of top.

![](img/579efec8c67772f31ecf34844bbb71a2_1171_0.png)

# Chapter 29 Performance Analysis

Chapter 24, Virtualization, for additional information about various virtualization technologies and their implications.

# How the system manages memory

The kernel manages memory in units called pages that are usually 4KiB or larger. It allocates virtual pages to processes as they request memory. Each virtual page is mapped to real storage, either to RAM or “backing store” on disk. (Backing store is usually in the swap area, but for pages that contain executable text, the backing store is the original executable file. For some data files it may be the files themselves.) The kernel uses a “page table” to keep track of the mappings between these made-up virtual pages and real pages of memory.

The kernel can effectively allocate as much memory as processes ask for augmenting RAM with swap space. Since processes expect virtual pages to map to real memory, the kernel may have to constantly shuffle pages between RAM as different pages are accessed. This activity is known as paging.

The kernel tries to manage the system’s memory so that pages that have been recently accessed are kept in memory and less pages are pushed out to disk. This scheme is an LRU system since the least recently used pages are the ones that get shunted to disk.

It would be inefficient for the kernel to keep track of all memory references, so it uses a cache-like algorithm to decide which pages to keep in memory. The algorithm varies by system, but the concept is similar across platforms. This system is cheaper than a true LRU system and produces comparable results.

When memory is low, the kernel tries to guess which pages on the inactive list were least used. If those pages have been modified by a process, they are considered “dirty” and must be pushed out to disk before the memory can be reused. Pages that have been laundered in this fashion (or were never dirty to begin with) are “clean” and can be recycled for use elsewhere.

When a process refers to a page on the inactive list, the kernel returns the page’s memory mapping to the page table, resets the page, and transfers it from the inactive list to the active list. Pages that have been written to disk must be pushed in before they are reactivated if the page in memory has been remapped. A “soft fault” occurs when a process references an in-memory inactive page and a “hard fault” results from a reference to a nonresident (p-out) page. In other words, a hard fault requires a page to be read from disk and a soft fault does not.

The kernel tries to stay ahead of the system’s demand for memory.
