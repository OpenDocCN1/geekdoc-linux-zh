# Checklist for Coping with New Kernels

When dealing with new kernels, keep the following items in mind:

+   - Building and running the kernel depends on the software versions listed in *linux/Documentation/Changes*. Before you compile or run any new kernel, you can save a lot of heartache if you check your system against these version numbers!

+   - Drivers bundled with Linux may not be the very latest. If you have problems with a particular device, or with very new hardware, search for an update before building your kernel.

+   - Kernel changes may require changes to your boot scripts, to */etc/lilo.conf*, or */etc/modules.conf*. The *linux/Documentation* collection contains many short *README* files on many different parts of the kernel, and each driver subdirectory may also contain additional information on installing or configuring difficult devices. Most kernel modules accept parameters either through the bootparameters, through the append line of */etc/lilo.conf*, or, for dynamically loaded modules, on the */sbin/insmod* command line or in */etc/modules.conf*.

+   - If you give options both in */etc/lilo.conf* and at the *LILO:* prompt, the boot prompt options are *appended* to the end of the append options. This allows you to override installed options at the command line to pre-empt unwanted settings; this is also why many modules also include options to restore their default behavior.