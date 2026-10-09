
their drivers. The GDI tailors its messages to the capabilities of the device, often dividing the request into manageable parts. For example, some devices can understand directions to draw an ellipse; others require the GDI to interpret the command as a series of pixels placed at certain coordinates. For more information about the graphics and video driver architecture, see the "Design Guide" section of the book *Graphics Drivers* in the Windows Device Driver Kit (DDK), available at www.microsoft.com/ddk.

**POSIX Subsystem.** POSIX, an acronym loosely defined as "a portable operating system interface based on Unix," refers to a collection of international standards for Unix-style operating system interfaces. The POSIX standards encourage vendors implementing Unix-style interfaces to make them compatible so that programmers can move their applications easily from one system to another.

Windows 2000 implements only one of the many POSIX standards, POSIX.1, formally known as ISO/IEC 9945-1:1990 or IEEE POSIX standard 1003.1-1990. This standard was included primarily to meet U.S. government procurement requirements set in the mid-to-late 1980s that mandated POSIX.1 compliance as specified in Federal Information Processing Standard (FIPS) 151-2, developed by the National Institute of Standards and Technology. Windows NT 3.5, 3.51, and 4 have been formally tested and certified according to FIPS 151-2.

Because POSIX.1 compliance was a mandatory goal for Windows 2000, the operating system was designed to ensure that the required base system support was present to allow for the implementation of a POSIX.1 subsystem (such as the *fork* function, which is implemented in the Windows 2000 executive, and the support for hard file links in the Windows 2000 file system). However, because POSIX.1 defines a limited set of services (such as process control, interprocess communication, and simple character cell I/O), the POSIX subsystem that comes with Windows 2000 isn't a complete programming environment. And because applications can't mix calls between subsystems on Windows 2000, by default, POSIX applications are limited to the strict set of services defined in POSIX.1. This restriction means that a POSIX executable on Windows 2000 can't create a thread or a window or use remote procedure calls (RPCs) or sockets.

To address this limitation, Microsoft provides a product called Interix, which includes an enhanced POSIX subsystem environment that provides nearly 2000 Unix functions and 300 Unix-like tools and utilities. (See www.microsoft.com/windows2000/interix/default.asp for more information on Microsoft Interix.) With this enhancement, it is more viable to port Unix applications to the POSIX subsystem. However, because the programs are still linked as POSIX executables, they cannot call Win32 functions.

To port Unix applications to Windows 2000 and allow the use of Win32 functions, you can purchase a Unix-to-Win32 porting library, such as the one included with the MKS *NUTCRACKER* Professional product available from Mortice Kern Systems Inc. (*www.mks.com*). With this approach, a Unix application can be recompiled and relinked as a Win32 executable and can slowly start to integrate calls to native Win32 functions. Another such library is available from *www.cygnus.com*. This site also provides ports of popular GNU development tools and utilities for Windows.

To compile and link a POSIX application in Windows 2000 requires the POSIX headers and libraries from the Platform SDK. POSIX executables are linked against the POSIX subsystem library, *Pxsdll.dll*. Because by default Windows 2000 is configured to start the POSIX subsystem on demand, the first time you run a POSIX application, the POSIX subsystem process (*Pxss.exe*) must be started. It remains running until the system reboots.

For more information about the POSIX subsystem and about porting Unix applications to Windows 2000, do a search for POSIX and Unix in MSDN Library (*msdn.microsoft.com*).

## OS/2 Subsystem

The OS/2 environment subsystem, like the built-in POSIX subsystem, is fairly limited in usefulness in that it supports only OS/2 1.2 16-bit character-based or video I/O (VIO) applications. Although Microsoft did sell a replacement OS/2 1.2 Presentation Manager subsystem for Windows NT 4, it didn’t support OS/2 2.x (or later) applications (and the replacement isn’t available for Windows 2000).

### Ntdll.dll

*Ntdll.dll* is a special system support library primarily for the use of subsystem DLLs. It contains two types of function:

- System service dispatch stubs to Windows 2000 executive system services
- Internal support functions used by subsystems, subsystem DLLs, and other native images

The first group of functions provides the interface to the Windows 2000 executive system services that can be called from user mode. There are more than two hundred such functions, such as *NtCreateFile* and *NtSetEvent*. As noted earlier, most of the capabilities of these functions are accessible through the Win32 API. (A number are not, however, and are for Microsoft internal use only.)

For each of these functions, NtDll contains an entry point with the same name. The code inside the function contains the architecture-specific instruction that causes a transition into kernel mode to invoke the system service dispatcher, which, after verifying some parameters, calls the actual kernel-mode system service that contains the real code inside Ntoskrnl.exe.

NtDll also contains many support functions, such as the image loader (functions that start with Ldr), the heap manager, and Win32 subsystem process communication functions (functions that start with Csr), as well as general runtime library routines (functions that start with Rt). It also contains the user-mode exception dispatcher.

### Executive

The Windows 2000 executive is the upper layer of Ntoskrnl.exe. (The kernel is the lower layer.) The executive includes the following types of function:

- Functions that are exported and callable from user mode. These functions are called system services and are exported via NtDll. Most of the services are accessible through the Win32 API or the APIs of another environment subsystem. A few services, however, aren't available through any documented subsystem function. (Examples include LPCs and various query functions such as NtQueryInformationxxx and specialized functions such as NtCreatePagingFile.)

- Functions that can be called only from kernel mode that are exported and documented in the Windows 2000 DDK or Windows 2000 Installable File System (IFS) Kit. (For information on the Windows 2000 IFS Kit, go to www.microsoft.com/dsk/ifs kit.)

- Functions that are exported and callable from kernel mode but are not documented in the Windows 2000 DDK or IFS Kit (such as the functions called by the boot video driver, which start with Inbv).

- Functions that are defined as global symbols but are not exported. These include internal support functions called within Ntoskrnl, such as those that start with Iop (internal I/O manager support functions) or Mi (internal memory management support functions).

- Functions that are internal to a module that are not defined as global symbols.

The executive contains the following major components:

- The configuration manager is responsible for implementing and managing the system registry.

- *The process and thread manager* creates and terminates processes and threads. The underlying support for processes and threads is implemented in the Windows 2000 kernel; the executive adds additional semantics and functions to these lower-level objects.

- *The security reference monitor* enforces security policies on the local computer. It guards operating system resources, performing runtime object protection and auditing.

- *The I/O manager* implements device-independent I/O and is responsible for dispatching to the appropriate device drivers for further processing.

- *The Plug and Play (PnP) manager* determines which drivers are required to support a particular device and loads those drivers. It retrieves the hardware resource requirements for each device during enumeration. Based on the resource requirements of each device, the PnP manager assigns the appropriate hardware resources such as I/O ports, IRQs, DMA channels, and memory locations. It is also responsible for sending proper event notification for device changes (addition or removal of a device) on the system.

- *The power manager* coordinates power events and generates power management I/O notifications to device drivers. When the system is idle, the power manager can be configured to reduce power consumption by putting the CPU to sleep. Changes in power consumption by individual devices are handled by device drivers but are coordinated by the power manager.

- *The WDM/Windows Management Instrumentation routines* enable device drivers to publish performance and configuration information and receive commands from the user-mode WMI service. Consumers of WMI information can be on the local machine or remote across the network.

- *The cache manager* improves the performance of file-based I/O by causing recently referenced disk data to reside in main memory for quick access (and by deferring disk writes by holding the updates in memory for a short time before sending them to the disk). As described shortly, it does this by using the memory manager’s support for mapped files.

- *The virtual memory manager* implements *virtual memory*, a memory management scheme that provides a large, private address space for each process that can exceed available physical memory. The memory manager also provides the underlying support for the cache manager.

In addition, the executive contains four main groups of support functions that are used by the executive components just listed.
