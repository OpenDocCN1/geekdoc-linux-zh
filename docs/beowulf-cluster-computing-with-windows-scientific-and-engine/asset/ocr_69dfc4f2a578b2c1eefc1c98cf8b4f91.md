![](bbox=[0.0, 0.17, 1.0, 0.49])

**Figure 4.2**
Address space layouts supported by Windows 2000.

Because most systems have much less physical memory than the total virtual memory in use by the running processes (2 GBytes or 3 GBytes for each process), the memory manager *transfers*, or *pages*, some of the memory contents to disk. Paging data to disk frees physical memory so that it can be used for other processes or for the operating system itself. When a thread accesses a virtual address that has been paged to disk, the virtual memory manager loads the information back into memory from disk. Applications don’t have to be altered in any way to take advantage of paging because hardware support enables the memory manager to page without the knowledge or assistance of processes or threads.

# 4.2.5 Processes, Threads, and Jobs

A Windows 2000 process comprises the following:

+   * A private *virtual address space*, which is a set of virtual memory addresses that the process can use
+   * An executable program, which defines initial code and data and is mapped into the process’s virtual address space
+   * A list of open handles to various system resources, such as semaphores, communication ports, and files, that are accessible to all threads in the process