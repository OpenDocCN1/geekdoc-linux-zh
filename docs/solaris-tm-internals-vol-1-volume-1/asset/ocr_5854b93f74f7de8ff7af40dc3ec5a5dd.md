+   - **qwriter_outer_thread** — STREAMS based; processes outer STREAMS syncq messages. One of these threads is created for every CPU on a system at boot time.

All kernel threads, even those threads listed above that are part of the operating system, need a process context to execute, in order to have the required software context state (for example, an address space). Kernel threads created by the operating system are linked to process 0 (PID 0) for contextual information. Process context is discussed in detail in Chapter 5.

# 4.3  Kernel Module Loading and Linking

Much of the kernel architecture is layered architecture, and many of the kernel's major subsystems call into a common set of lower-level services. In some respects, the kernel architecture is similar to that of a client/server application, except that the interfaces in this case are, for the most part, private to the kernel. That is, many of the callable routines are not public interfaces available for use for general application software development. The other obvious distinction is that the users of the services, or clients, in this context, are other kernel subsystems, as opposed to application code. Exceptions to the private interface generalization are those interfaces defined for device drivers and kernel STREAMS modules, which are documented as the Solaris Device Driver Interface (DDI) specifications, found in section 9 of the manual pages.

The kernel module loading facility serves as a good example of one such service. Several phases are involved in dynamic module loading.

+   1. Load the module (a binary object file) into memory.
+   2. Establish kernel address space mappings for module segments.
+   3. Link the module’s segments into the kernel.
+   4. Perform the module-type-specific *install* function.

The loadable module types are defined in `/usr/include/sys/modctl.h`; they are device drivers, system calls, file systems, miscellaneous modules, streams modules, scheduling classes, and exec modules (exec support for executable objects). For each of these module types, some specific kernel installation steps are required to complete the loading process. We will take a look at these shortly.

The steps involved in loading a module into the kernel are similar conceptually to what happens when a dynamically linked program is started under Solaris. That is, shared objects to which a binary is linked are dynamically loaded into memory and linked into the process’s address space during execution. The kernel exists in memory as a large, dynamically linked executable, with essentially the same address space segments that exist in any process running on the system: