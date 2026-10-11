
## Synchronization Primitives and Locks

lock is available or the lock is being held. If that process is not foolproof, a thread executing on one processor could issue a load on the lock, and while it is doing a test operation, another thread executing on another processor issues a lock call to get the same lock at the same time. If the lock is not held, both threads would assume that the lock is available and would issue a store to hold the lock. The atomic instructions prevent such a disaster from happening.

Another important consideration involves the visibility of the lock state to the processors when the lock value is changed. It is mandatory that all processors have a consistent view of data in memory. The most recent state of the lock must be visible to all processors on the system at all times.

The Solaris kernel employs several types of synchronization objects. Locks come in different forms. The most commonly used lock in the Solaris kernel is the mutex lock, which provides exclusive read and write access to data. RW locks are read/write for situations where multiple readers are allowed but only one writer is allowed at a time. Kernel semaphores are used in some areas of the kernel where a finite number of resources must be managed. Another type of mutex lock called a dispatcher lock is used by the kernel when access protection is required as well as protection from interrupts. Several hundred locks are defined in the kernel source code, but that number is not accurate. Because the actual number of locks that exist in a running system is dynamic and grows with the size of the system, it is impossible to guess how many are available at one time. Again, this feature is one of the primary attractions of Solaris 8. It is able to provide the scalability and scaling synchronization primitives dynamically according to the size of the kernel. It is quite possible to have thousands of locks on a large system. Much more can be written about locks, but it is not the intent of this book to present more than an overview.

A semaphore provides a method of synchronizing access to a shared resource by multiple processes or threads. It can be used as a binary lock for exclusive access. For concurrent access by multiple threads, it is used as a counter. Semaphores are used in very few areas of the operating system. When the semaphore is used as a counter, its value is initialized to the number of shared resources. Whenever a resource is used, the semaphore value is decreased to indicate that there is one less resource available. When the process completes, the semaphore value is incremented. When zero (0) is reached, the calling process knows that no resources are available. These functions are called P and V operations; the P operation attempts to access the semaphore and the V operation releases it. The Solaris kernel uses semaphores only when appropriate. The counting functions they provide make them compatible with the allocation of fixed amounts of resource.

## Directory Hierarchy

The Solaris kernel, being modular in design, does not originate on disk as a single binary object but is constructed in memory and loads during bootstrap operations. The object modules are well defined and live in a name space in the root and usr file directories. Core modules are split across multiple directories in one of three categories. These categories determine where the modules are placed in the directory hierarchy. The first category is platform and hardware independent. The second is platform dependent, and the third is hardware class dependent. The /directory tree contains operating system modules that load at boot time. Hardware class-dependent modules are derived from the processor type. You can determine the hardware class of a system by using the `uname(1)` command with the `-m` option. The platform-dependent category includes the type of system. The `-i` option will show hardware implementation. Solaris will usually be housed on Sun-based platforms such as SUNW, Ultra-S, and SUNW, and Enterprise. The kernel modules that deal with machine dependencies, reside in the directory tree that begins with `/platform/<platform-name>`.

Other kernel modules are located under the `/usr` directory. This tree also contains kernel (`/usr/kernel`) and platform (`usr/platform`) subdirectories. These modules are loaded on an as-needed basis.

> **TIP** You can request that the system load optional modules at boot by using the force=load directive in the `/etc/system` configuration file.

Only one `genunix` binary gets loaded when you boot the system; usually the SPARC version or the `/kernel/genunix` on all other systems. These include callback and callout facilities, clock and timer, kernel memory allocator, management routines, runtime linker, synchronization primitives, device driver interfaces, and kernel thread and lightweight process code.

These binary kernel modules, resident in memory, construct the kernel upon boot-up. The following sequence is based on a local disk boot; networkx use different boot programs:

- 1. The boot block is loaded into memory.
- 2. The secondary boot program is located and loaded into memory.
- 3. The `ufsboot` locates and loads the core kernel images and the runtime linker.
- 4. Mandatory modules are loaded from the root directory tree and execute startup code.
- 5. Kernel startup code creates and initializes structures, resources, and software.
- 6. System executes shell scripts from system directories.

Although the SPARC systems have been discussed, much of the initialization process is hardware independent once the boot phase is complete and the kernel is loaded. Control then passes to Unix, which is loaded near the top of physical memory space and takes over execution. The Memory Management Unit (MMU) is enabled and the first 16 megabytes of memory are mapped. Devices are then mapped. One of the first devices to be mapped is the Electrically Erasable Programmable Read Only Memory (EEPROM on SPARC), which holds the Open Boot Prom (OBP) code. It occupies a part of the physical address space. Calls into the PROM are required during the boot-up. PROM aids in the retrieval of hardware and version information. Once m1setup() work is finished, the kernel begins the function calls into the higher-level areas of the kernel. The main() function is entered. It calls into hardware routines for initialization steps and then returns to the common code to complete the boot process.

Although there are innumerable processes going on behind the scenes, you need only know that kernel module loading occurs at various points in the boot process. During the platform-specific startup, the swap, specfs, and procfs are loaded. Scheduling classes are loaded during the dispatch() function, which initializes the kernel dispatcher subsystem. Once the virtual memory support is initialized, the specfs and swapfs file system support modules are loaded and initialized. Kernel modules set for force load are loaded with the 'force load: /drv/foo' command in /etc/system and the kernel trap table is set. Housekeeping is performed, interrupt threads are created, initialization functions for subsystems are started, and the first init process for the user is created by the system. All further processes are forked by init.

## Linking

Kernel architecture is layered. Many of the kernel subsystems access a common set of lower-level services. The interfaces are not public for use with application software development but are private to the kernel itself. Device drivers and STREAMS modules are exceptions to this generalization. The dynamic loading process follows a prescribed path:

- 1. Loads the module into memory
- 2. Establishes kernel address mappings for segments
- 3. Links the module segments into the kernel
- 4. Perform the module's install function

Loadable module types are defined in /usr/include/sys/modctl.h. Included are file systems, device drivers, exec modules, systems calls, miscellaneous modules, and
