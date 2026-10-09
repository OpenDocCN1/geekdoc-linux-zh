For each of these functions, NtDll contains an entry point with the same name. The code inside the function contains the architecture-specific instruction that causes a transition into kernel mode to invoke the system service dispatcher, which, after verifying some parameters, calls the actual kernel-mode system service that contains the real code inside Ntoskrnl.exe.

NtDll also contains many support functions, such as the image loader (functions that start with Ldr), the heap manager, and Win32 subsystem process communication functions (functions that start with Csr), as well as general runtime library routines (functions that start with Rt). It also contains the user-mode exception dispatcher.

# 4.3.3  Executive

The Windows 2000 executive is the upper layer of Ntoskrnl.exe. (The kernel is the lower layer.) The executive includes the following types of function:

+   Functions that are exported and callable from user mode. These functions are called system services and are exported via NtDll. Most of the services are accessible through the Win32 API or the APIs of another environment subsystem. A few services, however, aren't available through any documented subsystem function. (Examples include LPCs and various query functions such as NtQueryInformationxxx and specialized functions such as NtCreatePagingFile. on.)

+   Functions that can be called only from kernel mode that are exported and documented in the Windows 2000 DDK or Windows 2000 Installable File System (IFS) Kit. (For information on the Windows 2000 IFS Kit, go to www.microsoft.com/dsk/ifs kit.)

+   Functions that are exported and callable from kernel mode but are not documented in the Windows 2000 DDK or IFS Kit (such as the functions called by the boot video driver, which start with Inbv).

+   Functions that are defined as global symbols but are not exported. These include internal support functions called within Ntoskrnl, such as those that start with Iop (internal I/O manager support functions) or Mi (internal memory management support functions).

+   Functions that are internal to a module that are not defined as global symbols.

The executive contains the following major components:

+   The configuration manager is responsible for implementing and managing the system registry.