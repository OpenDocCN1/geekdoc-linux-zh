built and installed. The build entry is a symlink to /usr/src/linux. The kernel directory contains all the modules below it. The pcmcia directory contains symlinks, which point to modules located below /kernel in various locations.

Below the kernel subdirectory are four major subdirectories: arch, drivers, fs, and net.

The arch directory will contain architecture-specific modules below their particular architecture. Modules like cpuid and apm will be found here in i386/kernel/.

The driver directory contains numerous subdirectories, but all modules located here are related to physical hardware. If you can touch it and you built a module for it, it’s located somewhere here below drivers.

The fs directory contains filesystem-specific drivers. These drivers handle any filesystems you compiled support for as modules. Often this would be modules such as vfat, msdos, and others.

The net directory contains all network-related modules that are not hardware based. Here you’ll find the ipv6 module, all the netfilter modules, the kernel httpd module (khttpd) and much more.

You can get a good idea of what modules are installed on your system by perusing the /lib/modules/`uname -r`/modules.dep file created by the kernel build.

# MODULE VERSIONS

By default, when recompiling a Linux kernel, all the modules that are to be loaded with the new kernel must be recompiled as well. This can become a tedious process, especially if the system on which the kernel is being compiled uses legacy hardware. Compilation of the kernel can take a long time on slow hardware, so cutting down on the time required to do a compilation is desirable.

However, an option by which modules can be reused without recompiling them is available during the kernel configuration process. If you activate the following option, version information is set on all modules that will allow non-kernel modules to be loaded with any kernel that matches the version of the kernel symbols against which the modules were compiled:

Set version information on all symbols and modules

In other words, a Linux kernel that is at version 2.4.1 loads modules compiled for 2.4.1 kernels as long as the symbols within the module are set at version 2.4.1 as well. In most cases, this will be fine because you will use modules built with your kernel. But if you don’t have the sources to compile kernel modules against your kernel, such as from a hardware manufacturer that only includes a binary module with their hardware, you might need to set version information so that it will load.