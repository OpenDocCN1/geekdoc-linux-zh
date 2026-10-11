The first of these two types of memory is physical memory. *Physical memory* is represented by the amount of memory in the server’s physical memory chips. Modern servers have large amounts of physical memory—2GB and 4GB of RAM are common. This available memory is divided up into smaller pieces called pages. Much like Oracle extents stored within tablespaces, the allocation of processes and data to these pages is managed by the operating system via a mechanism called a page table. If the physical memory pages are full, a server’s OS may have to temporarily remove pages or processes from memory in order to make room for other requested pages or processes. This process is referred to as paging or swapping. Table 10.2 compares paging and swapping.

**TABLE 10.2** Paging versus Swapping

| Paging | Swapping |
| :--- | :--- |
| An individual memory page is temporarily removed from memory and written to disk in order to make room for another requested page. | An entire process is removed from memory and written to disk in order to make room for another requested process or page. |

When paging or swapping occurs, the second type of memory, *virtual memory*, is used to store the on-disk copy of the page or process that was removed from physical memory. Much like Oracle SGA tuning, the primary goal of OS tuning is to maximize the frequency with which requested memory pages are already cached in memory when requested so that they do not need to be read from disk (i.e., virtual memory).

The techniques used to monitor paging and swapping vary by operation system. Table 10.3 shows examples of Unix commands that can be used to monitor paging and swapping. See your Unix man pages for details on the output returned from each of these commands.

**TABLE 10.3** Commands to Monitor Paging and Swapping on Unix Systems

| Command | Description |
| :--- | :--- |
| ipcs | Displays the virtual memory size of all shared segments on the server. |
| ps | Used with the -1 or -u flags, this command displays the amount of virtual memory used by an individual process. |