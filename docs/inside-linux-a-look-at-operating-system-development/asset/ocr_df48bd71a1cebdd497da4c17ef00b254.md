needs to load or create a page of memory and no frame is available to hold it. Once the kernel selects a victim page, that page is written to disk and the frame is available for a new page.

This approach yields high performance at a cost: because there is no assurance of a place on disk for each page of memory, it is possible to run out of storage for all the virtual memory. In matters such as this, Linux and most other Unix systems are a bit sloppy. Most users are willing, albeit unknowingly, to sacrifice some reliability for much greater performance. In this instance, it’s possible that the parent or child could fail at some later time when it attempts to write to a page and neither a physical frame nor disk swap space are available to save a copy. That program would fail and yield its allocation of physical memory and swap space back to the system.

# 5.4.3 Disk Caching

The other major use of memory is as a buffer for disk I/O.

All disk I/O pass through a uniform buffer mechanism which attempts to hold copies of disk data as long as possible—even after it has been written to disk. This provides the user with quick access to the data if a read is issued for disk data which is already held in the buffer.

The system balances the use of memory for buffer with the need for frames to hold virtual memory pages. Of course, virtual memory needs have precedence, but the kernel will attempt to use all the rest of the memory for buffering.

# 5.5 Security

The basic system security relies on several elements: processes are owned by a user and can belong to several different groups. The file system limits access to files, directories and devices based on a processes ownership and group membership. Each process has independent virtual address space (which can contain memory segments which are explicitly shared with other processes), but access to physical memory is generally forbidden.