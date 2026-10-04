
![](img/ad36c2db45661d7b3b68db09c8eea0a1_459_0.png)

## Figure 30.3 Paging allows easy memory segment growth.

thus selected contains the required 20-bit physical page number plus the other bits discussed previously.

Figure 30.2 illustrates this address translation arrangement from linear to physical addresses. Once again, if this translation were to be performed fully for each linear address access it would require an extra two memory reads to access the page directory and page table – a very expensive operation in terms of time. The solution used, as before, is to have some extra registers inside the CPU which are used to store the most recent address translations, making the lookup very much faster. These extra registers form the translation lookaside buffer (TLB).

### 30.2.1 Segment Growth

Paging is very useful in the situation where you wish to increase the size of a memory segment which is boxed-in in physical memory. Figure 30.3 illustrates the point.

Part (a) shows two memory segments composed of several pages which are mapped into the physical memory pages on the right of the diagram. Notice how, in physical memory, the pages for segment 1 are enclosed by the pages used for segment 2. Without paging, it would not be possible to increase the size of segment 1 without moving the entire segment to a new area of contiguous physical memory that was large enough to contain the enlarged segment.

Part (b) shows that, with paging, enlarging the size of segment 1 is a simple task as contiguous pages in the linear address space of segment 1 do not need to be physically contiguous, so that the new page (linear page 3) can just be allocated any free physical page, which just gets mapped to make it appear in the right place in segment 1.

### 30.2.2 Swapping

The other main use for paging is called swapping (it is called this for historical reasons – old versions of UNIX). The idea behind swapping is that it is possible to have more processes running on the system than could possibly fit into memory at the same time. This involves setting aside an area of swap space (usually on disk) to act like a memory overflow area. When you wanted to start up a new process and there was not enough room in memory to do so, the swapper would be called, which would chose one or more of the processes currently in memory to be written to the swap space in order to make room for the new process to be loaded and run. As processes progress some will block waiting for I/O and others will terminate. This gives the opportunity to bring swapped out processes back into memory (maybe at the expense of other processes being swapped out) so that they can continue their execution.

Using paging to perform the swapping function means that you do not need to swap out entire processes to disk, but only enough pages to make room for the new process to run. In fact, in Linux it is even better than that because it uses a technique called demand paging. In order for demand paging to work, the entries in the page tables need to contain information to say whether or not the contents of the pages to which the entries point are actually loaded into memory or not. With this information available, whenever the CPU tries to access a physical memory page which is not present in memory, an exception can be raised (called a page fault). This exception forces a call to an exception handler which will load the page into physical memory. The instruction which caused the page fault can then be restarted, and this time it should succeed.

This is such a good idea that new processes can be loaded into memory using the technique (and Linux does). What happens is that whenever the running process tries to execute an instruction at an address which is not yet loaded, a page fault occurs and is dealt with, after which the process can continue.

Studies on executing code soon reveal that for reasonable-sized programs a large proportion of the code does not get executed on any particular run. With demand paging, the implication of this is that, after a while, the process will have loaded the pages it requires and it will settle down to running with few new page faults and also with many of its pages not loaded into memory at all. Even if a particular program run does require access to all the program pages, then at any one time and for a significant length of time the process is typically only using a small subset of the pages, so that paging still reaps huge benefits.

## 30.3 Linux Specifics

The only way to start a new process under Linux is to use the fork() system call. This starts off by allocating two pages of memory, one for the task structure associated with the new process and one for use as stack space in the kernel when the kernel is running on behalf of the new process.

Next, the child task structure is copied from the parent, and some changes are made to set up the necessary differences such as process ID and session leadership. Finally, all the process information, including the memory map, is copied across to the new child. The child process has its own local descriptor table (LDT) and, therefore, its own text data and stack segments and it also has its own page tables which initially are just a copy of the parent’s tables. The fork() call conceptually makes the child a copy of the parent’s text, data and stack segments. However, this would be an expensive operation in terms of time, especially when in all probability the child is going to execute an exec() system call almost immediately and replace the contents of these segments with those belonging to a new program. To overcome this waste, Linux only copies the page tables from parent to child and not the pages to which they give access.

In the case of the text segment, this technique is fine as the text segment is flagged as read only anyway and the two processes cannot tell, just by reading, that they are sharing the code. However, the data and stack segment is read-write so sharing here will cause problems as soon as one of the processes wants to write some data. The Linux solution to this problem is called copy on write. What happens is that whenever one of the processes wants to write to a data or stack page that is currently shared, that page is copied and the page tables are updated so that each process now has its own copy of that page and can write to it without interfering with the other process.

When the exec() system call is used to start off a new program, then demand paging is used to load the pages needed for the process to run.

There are many occasions when new memory pages need to be allocated to a process. Eventually, the free page list will become exhausted. At this point Linux will try to steal a page from somewhere else, writing it to swap space if necessary, in order to satisfy the request. The possibilities for obtaining a page include reducing the number of pages used for disk buffer cache, as the boundary between buffer cache memory and ordinary process memory is dynamic in Linux. If it is necessary to steal a page of process memory to satisfy the memory request, then choosing to steal a page from the text segment of some process means that it doesn’t need to be written out to swap space before it is freed as it is read-only (so it can’t have changed) and it can be demand paged back in again from the original executable file.

## Filestore

In order to access the contents of a filesystem under Linux it is necessary to mount that file system into the directory hierarchy. You have already seen that this is done with the mount command. What we have not seen, however, is that there are many filesystem types, any or all of which can be mounted in any combination, almost without limit.

### 31.1 VFS

It is the job of the Virtual Filesystem Switch (VFS) to make it possible for Linux to be able to mount and access all of the various filesystem types. The main task of the VFS is effectively to add a layer of indirection into the Linux filestore to switch filesystem calls to the appropriate routines in the code for the correct filesystem type.

There are many filesystem types currently supported by Linux via the VFS, these include:

- **minix** This is the earliest filesystem type supported by Linux; indeed, originally, it was the only supported filesystem type. Its two main disadvantages are that it only supports disk partitions up to 64Mb and it only allows file names up to 14 characters long.
- **ext** The extended filesystem was soon added to Linux and it overcame the problems with the minix filesystem by offering disk partitions up to 2Gb and file names up to 255 characters in length. However, it had its own problems in terms of facilities and performance and was soon superseded.
- **xiafs** This was one of two main attempts to replace the Ext filesystem and was based largely on the minix filesystem but with extensions to overcome its problems. However, Xiafs soon lost its popularity in favor of another filesystem type with greatly improved performance and facilities.
