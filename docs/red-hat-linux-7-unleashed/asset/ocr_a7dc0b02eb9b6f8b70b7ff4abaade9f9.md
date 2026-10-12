# High Memory Support

Linux will support up to 64 gigabytes of RAM, but this support must invoke Intel Physical Address Extensions (PAE) to use memory above the 4GB limit. All Intel Pentium series CPUs and the new ia64 support PAE, but enabling this option will crash on CPUs that do not support PAE. For systems with up to 1GB of RAM, no special options are required, and for systems with between 1GB and 4GB of RAM, the 4GB option will split memory into a 3GB space useable by other applications and a 1GB region for internal use by the kernel.

> **Memory Technology Devices**
> 
> If your CPU cannot cache all the memory on your machine, you can still use this memory for swap or storage through the Memory Technology Device (MTD) option. This option is primarily intended for “flash” cards and the “disk on a chip” components used in embedded applications, but can also be used to gain access to this inaccessible memory.

# SMP and IO-APIC

With the 2.4 kernels, SMP will support up to 16 processors on Intel x86 machines; SMP support for other architectures is still considered experimental.

Symmetric Multi-Processing (SMP) can have some unexpected side effects and enabling this option can restrict the portability of your kernel. Whereas a non-SMP kernel will run on a multi-CPU machine (but will use only one processor), an SMP kernel will slow a single CPU machine, hang on ix86 machines, and different architectures such as Pentium III versus Pentium Pro will not run the same SMP code. SMP will also require the Enhanced Real Time Clock Support and will disable Advanced Power Management; you may also need to set your BIOS options for Unispare. For more information on SMP support, look up the SMP-FAQ (http://www.lriae.fr/~/pmire/membre/smp-faq/).

The Advanced Programmable Interrupt Controller options APIC and IO-APIC are generally related to SMP machines but may be supported on some single-processor boards; the option will not slow the kernel if your hardware lacks this support, so it is safe to set this option, and this support will be automatically included if you select SMP.

# Loadable Module Support

It is hard to imagine a circumstance in which you would not want to include module support and enable the kernel module loader. For most situations, module support allows the kernel to support many devices and filesystems without incurring the overhead of