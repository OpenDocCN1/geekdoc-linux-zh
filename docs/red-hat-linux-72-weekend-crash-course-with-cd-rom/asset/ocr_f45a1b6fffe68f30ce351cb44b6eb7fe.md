```
```
sep_bug                : no
fdo_bug                : yes
fpu                    : yes
fpu_exception          : yes
cpuid level            : 1
wp                     : yes
flags                  : fpu vme de pse tsc msr mce cx8 mmm
bogomips               : 398.13
```
```

This output is from a 200MHz Pentium MMX system. The listing shows many interesting characteristics of the processor. Notice the line that starts with fdiv_bug. Remember Intel's infamous Pentium Floating-point division bug! The bug is in an instruction called fdiv (for floating-point division). Thus, the fdiv_bug line indicates whether this particular Pentium has the bug. Fortunately, it does not.

The last line in the /proc/cpuinfo file shows the BogoMips for the processor, as computed by the Linux kernel when it boots. The BogoMips value is a measure of CPU speed that Linux uses internally to calibrate time delay loops but that has no real meaning in terms of comparisons between CPUs of different speeds or between different systems.

Table 28-2 summarizes some of the files in the /proc file system from which you can get information about your Red Hat Linux system. You can view some of these files on your system to see what they contain.

> > Not all the files shown in Table 28-2 are present on your system. The contents of the /proc file system depend on the kernel configuration and the loaded driver modules (which, in turn, depend on your PC's hardware configuration).

Table 28-2  *Some Files and Directories in /proc*

| Filename | Contents |
|---|---|
| /proc/apm | Information about advanced power management (APM). |
| /proc/bus | Directory with bus-specific information for each bus type, such as PCI. |
| /proc/cmdline | The command line used to start the Linux kernel (for example, auto BOOT_IMAGE=linux no root=303). |
| /proc/cpuinfo | Information about the CPU (the microprocessor). |
| /proc/devices | Available block and character devices in your system. |
| /proc/dma | Information about DMA (direct memory access) channels in use. |
| /proc/filsystems | List of supported file systems. |
| /proc/ide | Directory containing information about IDE devices.

*（continued）*