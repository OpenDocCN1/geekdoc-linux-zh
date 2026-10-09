![](bbox=[0.15, 0.08, 0.85, 0.34])

Figure 2-4. *Architecture of a generic Linux system*

+   * Linux normally requires at least a 32-bit CPU containing a memory management unit (MMU).†
+   * A sufficient amount of RAM must be available to accomodate the system. Requirements will be laid out in later chapters.
+   * Minimal I/O capabilities are required if any development is to be carried out on the target with reasonable debugging facilities. This is also very important for any later troubleshooting in the field.
+   * The kernel must be able to load a root filesystem through some form of permanent storage, or access it over a network.

See “Types of Embedded Linux Systems” in Chapter 1 for a discussion of typical system configurations.

Immediately above the hardware sits the kernel, the core component of the operating system. Its purpose is to manage the hardware in a coherent manner while providing familiar high-level abstractions to user-level software (such as the POSIX APIs and the other de facto, industry-standard APIs against which applications are generally written). As with other Unix-like kernels, Linux drives the devices, manages I/O access, controls process scheduling, enforces memory sharing, handles the distribution of signals, and tends to other administrative tasks. It is expected that applications using the APIs provided by a kernel will be portable among the various architectures supported by this kernel with little or no changes. This is usually the case with Linux, as can be seen by the body of applications uniformly available on all architectures it supports.

† As we’ll see, the official Linux kernel includes the fruits of a project known as uClinux which runs on some CPUs that aren’t equipped with full MMUs. However, the development of applications for Linux on such processors differs sufficiently from standard Linux application development to require a separate discussion. Because of this, plus a relative lack of widely available software for such systems, we do not cover the use of Linux on MMU-less architectures.