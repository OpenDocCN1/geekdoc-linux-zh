Figure 4.3 illustrates the boot flow up to this point, using the sun4u (Ultra-SPARC) directory hierarchy for the example.

![](bbox=[0.168, 0.175, 0.953, 0.403])

Figure 4.3 Boot Process

# 4.2.5 Creating Kernel Structures, Resources, and platmod, and the CPU Components

With all the core binary objects (unix, krtld, genunix, kernel module) loaded into memory and linked, krtld passes control to unix, which is loaded near the top of physical memory space, to take over execution. The Solaris kernel is now running, the Memory Management Unit (MMU) is enabled (the code is generating virtual addresses and working in virtual address space), and the first 16 megabytes of memory are mapped. unix does some low-level setup of processor registers, begins hand-crafting kernel thread 0, and calls an architecture-specific startup function, mlset(1). mlset() completes the initialization of kernel thread 0 and LWP 0, builds the first process (p0), and begins mapping system devices to device information in the OBP space.

The EEPROM on SPARC systems, which holds the OBP code, is one of the early devices mapped. That is, the eep occupies a part of the system's physical address space, much like a physical device. A kernel software layer is initialized, very similar to a device driver, allowing other areas of the kernel to call into the PROM. Calls into the PROM are required during the boot process for a variety of reasons, such as the retrieval of hardware and version information.

With the mlset() work done, the kernel main() function is entered, which is where the code begins a sequence of function calls into the higher-level areas of the kernel to continue the initialization process. The main() function is part of the kernel hardware-independent code. It immediately calls into hardware-specific routines for specific initialization steps, then returns to the common code to complete the boot process.