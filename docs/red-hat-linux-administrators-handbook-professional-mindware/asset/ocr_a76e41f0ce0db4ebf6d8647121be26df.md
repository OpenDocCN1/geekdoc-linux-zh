If you have multiple processors on your system and want to turn on symmetric multiprocessing support, choose the default. In my case, I do not have a motherboard with multiprocessors; therefore, I chose “n” to decline SMP support.

# Loadable module support

The Linux kernel uses an innovative method for keeping a low profile. It uses features and drivers implemented as external modules. The modules are dynamically loaded and unloaded on an as-needed basis. This allows the kernel to require less memory and to become more hardware independent. Typically, you load the modules by using a program called kerneld, which, in turn, uses another program called modprobe to manage available modules, and so on. Modules can be device drivers, file systems, binary executable formats, and so on. In this section, you are asked if you want module-related support or not. The first question is as follows:

**Enable loadable module support (CONFIG_MODULES) [y/n/?]**

This really should not be a prompt because you definitely want to have loadable module support for almost all scenarios. The default is fine.

Set version information on all symbols for modules (CONFIG_MODVERSIONS) [N/y/?]

When you compile modules with version information, you can reuse them with new kernels without needing to compile them from scratch. However, the preferred method is to compile the modules along with the new kernel to eliminate compatibility problems. Hence, the default option to not include the version information is sufficient.

**Kernel module loader (CONFIG_KMOD) [N/y/?]**

Again, you load modules by using the kernel program. This prompt asks if you would like to use a module loader inside the kernel itself to avoid using the kmod daemon. Either way, modules are loaded automatically, so this does not make much difference.

# General setup

In this section, you configure the general options.

**BIGMEM support (CONFIG_BIGMEM) [N/y/?]**