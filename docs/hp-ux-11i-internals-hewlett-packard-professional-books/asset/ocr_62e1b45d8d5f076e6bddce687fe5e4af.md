the kernel. To move away from this dependency, a virtual file system interface was designed and implemented in the kernel.

The virtual file system treats all file system types the same. It is primarily concerned with their type, where they are mounted, a pointer to core-resident copies of any metadata that may be required to manage them, a cached copy of their respective root directories, and a pointer to an operational array of routines customized to handle their specific type.

# The Inode Cache

The inode is the heart and soul of a UNIX file; it contains all attribute information with respect to a specific file. As the file is the basic object of all I/O operations, the inode attribute information is the key to access rights and data security within the system.

File attribute information is needed each time a thread requests access to file data or to modify the inode data itself. To speed this operation, an in-core copy is maintained of the inode data for each open file on the system. This is known as an inode cache.

As each file system type may define different inode data structures (different sizes, different block location schemes, different immediate data storage methods), it is the job of each configured file system type to define and build its own inode cache. To mask this difference from the higher levels of the kernel, an abstraction layer is added in which each file has assigned to it a systemwide unique virtual node (or vnode). Actions aimed at the vnode are translated through an operations array to file system type-specific routines in the kernel.

# The Buffer Cache

Just as we keep copies of file attributes in an inode cache, the system maintains and manages a memory-resident buffer cache to hold recently requested copies of file data. When a process requests a read or write of file data, the buffer cache is checked first to see if a copy is present. If a cached copy is present, then the system merely needs to perform a memory-to-memory transfer of the requested buffer to or from the program's data space. Memory-to-memory transfers of this nature are called logical reads or logical writes. If a requested buffer is not present or the buffer is filled, a transfer must take place between the buffer cache and the physical disk. This constitutes a physical read or physical write.

When a read or write request results in an immediate physical action, it is said to be a buffer cache miss. The ratio between logical and physical reads and writes is called the hit rate and may be viewed using tools such as HP's glance or gpm.

# The Kernel Input/Output Tables

The HP-UX kernel allows no direct access to physical devices. All I/O must be requested through the proper channel: the system call interface. A key component of this model is the ker-