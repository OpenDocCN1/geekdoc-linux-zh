+   • Be a great distributed computing platform, both as a network client and as a server.
+   • Run most existing 16-bit MS-DOS and Microsoft Windows 3.1 applications.
+   • Meet government requirements for POSIX 1003.1 compliance.
+   • Meet government and industry requirements for operating system security.
+   • Be easily adaptable to the global market by supporting Unicode.

The following sections expand on how these goals were met by the design and implementation of the system.

# ### 4.2.1 Memory Protection Model

Windows 2000 is similar to most Unix systems in that it is a monolithic operating system in the sense that the bulk of the operating system and device driver code shares the same protected memory space. Windows 2000 isn't a microkernel-based operating system in the classic definition of microkernel (although some claim it as such), where the principal operating system components (such as the memory manager, process manager, and I/O manager) run as separate processes in their own private address spaces, layered on a primitive set of services the microkernel provides.

All these operating system components are, of course, fully protected from errant applications because applications don't have direct access to the code and data of the privileged part of the operating system (though they can quickly call other kernel services).

In most multiprocessor operating systems, applications are separated from the operating system itself—the operating system code runs in a privileged processor mode (referred to as *kernel mode* in this book), with access to system data and to the hardware; application code runs in a nonprivileged processor mode (called *user mode*), with a limited set of interfaces available, limited access to system data, and no direct access to hardware. When a user-mode program calls a system service, the processor traps the call and then switches the calling thread to kernel mode. When the system service completes, the operating system switches the thread context back to user mode and allows the caller to continue.

This protection is one of the reasons that Windows 2000 has the reputation for being robust and stable both as an application server and as a workstation platform, yet fast and nimble from the perspective of core operating system services, such as virtual memory management, file I/O, and networking.

The kernel-mode components of Windows 2000 also embody basic object-oriented design principles. For example, they don't reach into one another's data structures