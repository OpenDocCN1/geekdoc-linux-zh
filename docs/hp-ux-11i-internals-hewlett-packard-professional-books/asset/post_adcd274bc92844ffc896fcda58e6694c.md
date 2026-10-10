
The kernel. To move away from this dependency, a virtual file system interface was designed and implemented in the kernel.

The virtual file system treats all file system types the same. It is primarily concerned with their type, where they are mounted, a pointer to core-resident copies of any metadata that may be required to manage them, a cached copy of their respective root directories, and a pointer to an operational array of routines customized to handle their specific type.

### The Inode Cache

The inode is the heart and soul of a UNIX file; it contains all attribute information with respect to a specific file. As the file is the basic object of all I/O operations, the inode attribute information is the key to access rights and data security within the system.

File attribute information is needed each time a thread requests access to file data or to modify the inode data itself. To speed this operation, an in-core copy is maintained of the inode data for each open file on the system. This is known as an inode cache.

As each file system type may define different inode data structures (different sizes, different block location schemes, different immediate data storage methods), it is the job of each configured file system type to define and build its own inode cache. To mask this difference from the higher levels of the kernel, an abstraction layer is added in which each file has assigned to it a systemwide unique virtual node (or vnode). Actions aimed at the vnode are translated through an operations array to file system type-specific routines in the kernel.

### The Buffer Cache

Just as we keep copies of file attributes in an inode cache, the system maintains and manages a memory-resident buffer cache to hold recently requested copies of file data. When a process requests a read or write of file data, the buffer cache is checked first to see if a copy is present. If a cached copy is present, then the system merely needs to perform a memory-to-memory transfer of the requested buffer to or from the program's data space. Memory-to-memory transfers of this nature are called logical reads or logical writes. If a requested buffer is not present or the buffer is filled, a transfer must take place between the buffer cache and the physical disk. This constitutes a physical read or physical write.

When a read or write request results in an immediate physical action, it is said to be a buffer cache miss. The ratio between logical and physical reads and writes is called the hit rate and may be viewed using tools such as HP's glance or gpm.

### The Kernel Input/Output Tables

The HP-UX kernel allows no direct access to physical devices. All I/O must be requested through the proper channel: the system call interface. A key component of this model is the kernel's extensive set of drivers, device maps, and the overall system's general input/output (I/O) system.

A large portion of the kernel memory space is occupied by these various components. The modern HP-UX kernel provides for the dynamic mapping of some of these should it be required.

#### The I/O Tree

A key table is appropriately named the *I/O tree*. This tree structure is actually a collection of linked objects used to identify and map system hardware devices to specific software drivers. The tree's roots stretch back to the system initialization, occurring even before the HP-UX kernel is loaded into memory. A subsection of this structure is the more elemental kernel *I/O tree* and is created in memory visible to the processor-dependent code (sometimes called the *bootrom*) to be used in the event of a system crash.

The individual nodes of the *I/O tree* contain basic information about the hardware address: its type, which software has claimed it (driver association), and which context it belongs to. Additional properties, such as a kernel-assigned instance number and pointers to its parent, siblings, and children, are also present.

The *I/O tree* follows an object model: nodes lower down in the tree structure inherit attributes from their parents and pass them on to their children. We explore this fully in Chapter 10, "I/O and Device Management."

#### System Interruptions

In addition to the *I/O* tree, the *I/O* subsystem is responsible for the detection and response to interruptions. You may notice that we use the word *interruption*, not *interrupts*: HP-UX describes all categories of events affecting normal processor execution as being *system interruptions*. They are broken into four categories: faults, traps, *interrupts*, and clocks.

To further complicate the topic, there are internal (CPU hardware, clocks, timers, etc.) and external (*I/O* devices, interface cards, physical device) *interrupts*, not to mention process signal handling.

As shown in Figure 3-14, internal *interrupts* are registered by a CPU and cause a vectored branch to memory-resident handling routines contained in an array called the *interrupt vector table* (IVT). Each entry in this table consists of a 32-byte block of code in which the initial portion of the *interrupt* handler must be loaded. Also note that control register *CR14* contains the *interrupt* vector address (IVA), the starting address of the IVT. As each physical processor maintains its own register set, it would be possible to have *interrupt* handlers specific to each processor. This is not generally the case, but it is an interesting option.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_113_0.png)

Figure 3-14 Kernel I/O Tables

An interesting interruption (registered as internal interrupt #4) is called the *external interrupt* and evokes routines vectored through an array named the *external interrupt receipt register switch table*, or simply the `eirr_switch[x]`. In most cases, this vectored switch table points toward the interrupt handling routine entry points associated with the kernel’s various hardware drivers. Two additional control registers assist in registering and enabling the various external interrupts: CR23 (the `eirr`) and CR15 (the external interrupt enabling mask, or `eierm`).

### Drivers and Switch Tables

The bottom portion of Figure 3-14 shows two switch tables. One is used for accessing block device drivers and the other for raw device drivers. A raw device is one to which data is transferred in byte streams of varying sizes.

A raw device may receive a single byte or many megabytes in a single transfer (or even gigabytes in today’s computing climate). Raw device access is also used to talk to and configure device controllers and interface cards when necessary.

Block devices hold mountable file systems. All I/O to a block device is directed through the system’s buffer cache to reduce physical requests to logical requests whenever possible for speed and convenience.

As drivers are built into the kernel image or registered for future dynamic loading, they are assigned a driver number, often called their *major* number. Many of the major numbers are reserved and always assigned to a specific driver; for example, the logical volume manager pseudo-driver is always assigned major number 64, while others are assigned from a dynamic pool of available numbers. This major number is visible through the `ll` or `ls -l` commands. To list all the currently used major numbers for an HP-UX kernel, enter the `lsdev` command. In general, many more devices have raw drivers than have block drivers.

The device switch tables are arrays of operational pointers. Each entry in the table consists of a subarray of jump points. The routines pointed to are entered in a documented order and cover actions such as open, close, read, write, and several more. If it sounds like we are talking about file I/O, you are absolutely correct—but remember that in the world of HP-UX (and UNIX in general), all types of I/O are treated like file I/O. No matter what type of physical device a driver was created to work with, to system process threads, first you open it, then you read or write to it, and when you are through you close it!

### Summary

This concludes our first pass through the kernel designer's tool kit. Knowledge of these structures and tables and how they work will help prepare us for an in-depth examination of the HP-UX kernel. HP-UX and UNIX in general have many nooks and crannies to be explored and understood. Please reference the generic algorithm explanations offered in this chapter as we encounter specific examples of their usage in the chapters to come.
