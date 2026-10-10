network traffic from server to client.

+   *remote_nfs_swap*  Enable or disable swap to mounted remote NFS file system. Used on cluster clients for swapping to NFS-mounted server file systems.

+   *swapmem_on*  Enable or disable pseudo-swap allocation. This allows systems with large installed memory to allocate memory space as well as disk swap space for virtual memory use instead of restricting availability to defined disk swap area.

+   *swchunk*  Defines amount of space allocated for each !!chunk!! of swap area. Chunks are allocated from device to device by the kernel. Changing this parameter requires extensive knowledge of system internals. Without such knowledge, Do not change this parameter from the normal default value.

# Variable-Page-Size Parameters

+   *vps_ceiling*  Defines the maximum system-selected page size if the user does not specify a page size.

+   *vps_chartr_ceiling*  Defines the maximum page size a user can specify by using the *chartr* command in a program.

+   *page_size*  Defines the default minimum user page-size if no page size is specified using *chartr*.

# Overview of Memory Paging Parameters

Configurable kernel parameters for memory paging enforce operating rules and limits related to virtual memory (swap space). They fall into the following categories:

+   Total System Swap  Maximum swap space that can be allocated system-wide.

+   Device Swap  Swap space allocated on hard disk devices.