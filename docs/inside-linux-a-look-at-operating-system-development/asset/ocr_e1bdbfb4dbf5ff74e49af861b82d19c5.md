Video I/O is commonly performed in this manner, although the GGI23 project intends to offer a more protected access to the display.

# ## 5.4 Memory Management

Once the system kernel has been loaded, all unused memory becomes a resource which can be shared among the processes. (In the case of some micro-kernel systems, the rest of the kernel will provide additional processes competing for the dynamically allocated memory.) Memory use falls into two general categories: that which is visible to the processes and that which is used on behalf of the processes.

# ### 5.4.1 Virtual Memory

Any virtual memory system must be built from a set of resource allocation policies which decide when to bring a page into memory (Fetch), where to put it (Placement and Replacement), when to write dirty pages to storage (Cleaning), how much physical memory a process is allowed (Allocation), and how many processes can share the system (Load Control).

# #### Fetch

The most common fetch policy is *demand paging*. This policy loads a page only when it is required. Locality of reference suggests that if a page is needed in memory, its neighboring pages may be needed as well. However, *prepaging* hasn't proven to be that useful except when restoring a process which was swapped out.

# #### Placement

In the case of segmented memory, placement is a very important issue. Figure 4.13 showed how good placement decisions could maintain larger chunks of unallocated physical memory. Research in this area,