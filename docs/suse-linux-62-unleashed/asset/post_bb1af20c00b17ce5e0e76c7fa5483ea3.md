
# Kernel Management
CHAPTER 23

For your first time through, you can use the defaults or the recommended option in the associated HELP page. Or, if you're feeling zealous, keep your computer manuals nearby or run your first configuration with the panels taken off your computer and a flashlight in hand.

Take heart—it is not absolutely essential that you match your computer chipset perfectly on your first kernel configuration. The defaults have served you well so far.

# Code Maturity Level

Although a stable kernel release such as the 2.2 series is considered to be ready for prime time, the kernel will still offer some features that are deemed experimental. These features may support new technology for which the standard has not yet been resolved, or they may offer new techniques which were considered essential enough to include but were not thought to be stable at the time of the release.

All these features are clearly marked as experimental so that Linux users won't use without knowing what they are doing. Users are invited to test these new features, report on their results, and file proper bugs, but are not asked to flood the mailing lists and newsgroups with complaints.

FIGURE 23.1
The xconfig kernel configuration panel.

| Linux Kernel Configuration | SDA subsystem support | Partition Types |
|---|---|---|
| Code maturity level options | | Native Language Support |
| Processor type and features | | Kernel drivers |
| Loadable module support | ISDN subsystem | Console drivers |
| General setup | Old CD-ROM drivers (not SCSI IDE) | Sound |
| Plug and Play support | Character devices | Additional low level sound drivers |
| Block devices | Watchdog Cards | Kernel hacking |
| Networking options | Video For Linux | |
| OS exit/or leaving queuing | Joystick support | Save and Exit |
| SCSI low-level drivers | Place the floppy tape device driver | Gut Without Saving |
| Network device support | Filesystems | Load Configuration from File |
| Amateur Radio support | Network File Systems | Store Configuration to File |

![](img/cbac72550c7126a22162e94d91a0c360_706_0.png)

Alpha-release drivers should not be considered to be only for the brave or the foolish. In some cases, “experimental” code may be essential to your purpose, such as Amiga filesystem support or enhanced support for certain PCI subsystems. It is the real-world testing of these features that is worth most to the developers. The main caveat here is that if your kernel fails midstream, you should remove all experimental modules before you suspect you found a bug among the stable modules.

# Processor Type and Features

Most distributions are preset for the safest setting: the old Intel 386 computer. This may be the first kernel option you will change.

When you're selecting the processor type, keep in mind that compiling for an advanced CPU may mean your kernel will not boot or fail on an older machine. This is also true for excluding the floating-point coprocessor emulation. A 386-SX may not run if the emulator is missing. Table 23.1 shows the recommended mapping of processor types to options.

| Kernel | Recommended CPU Option |
|---|---|
| 386 | AMD/Cyrix/Intel 386DX/DXL/SL/SX, Cyrix/TL |
| 486 | DLC/DLC2 and UMC 486SX-S. Only 386 kernels will run on an i386 machine |
| 486 | For the AMD/Cyrix/IBM/Intel Dx4 or 486DX/DX2/SL/SX/SX2, AMD/Cyrix 586, NexGen Nx586, and most U5 or US |
| 586 | Generic Pentium/Pentium MMX, possibly lacking the timestamp counter register |
| Pentium | Intel Pentium MMX, AMD K5, K6, and K63 |
| Pro | Cyrix/IBM/National Semiconductor 6x86MX, MII and Pentium II/III/Pentium Pro, as well as the AMD Athlon processor |

# MTRR and SMP

For Pentium Pro/II/III machines, Linux includes optional support for the Memory Type Range Register (MTRR). When this option is supported by the hardware and software, it can double the performance of video transfers. To use MTRR, you will need an X-Server that is aware of the interface through ioctl() calls or the /proc/mtr pseudo-file. You can query your MTRR system through /proc/mtr, and code for manipulating the interface is provided in linux/Documentation/mtrr.txt. An initialization bug on some Symmetric Multi-Processor (SMP) can also be corrected by including MTRR support.

# Kernel Management
CHAPTER 23 673

The last processor feature option enables support for SMP. With the 2.2 kernels, SMP support for up to 16 processors on Intel x86 machines is now a standard feature and is not experimental—support for up to 64 processors is expected soon may be in general release by the time this book is published. While Intel-platform SMP is fairly well defined in the 2.2 kernels, it is more refined in the 2.3 versions, and the support for other architectures is still considered experimental. For many enterprise applications, SMP support will be a primary reason for upgrading to Linux 2.3 or 2.4.

> Tip
> If you require SMP support, you will also need to include the Real Time Clock option under Character Devices.

On machines with only one CPU, SMP support can degrade performance and may not on some hardware. Deselecting this option for machines with more than one CPU will cause issues. For more information on SMP, look up the SMP-faq.

![](img/cbac72550c7126a22162e94d91a0c360_708_0.png)

# Loadable Module Support

It is hard to imagine a circumstance in which you would not want to include module support. For most situations, it allows the kernel to support many devices without the overhead of including this at all. In some situations, incompatible modules can share the port.

Modules are usually loaded by init-scripts or other shells that explicitly call insmod and rmmod to load and unload as needed. The 2.2 kernel now includes support for automatically loading modules. When the kernel detects a missing module, it will use the program specified in /proc/sys/kernel/modprobe to load the module. To clear out unused modules, you will need to rmmod -a or schedule it through root crontab entry:

0*/5 * * * /bin/rmmod -a

# General Setup

General setup includes enabling networking, PCI hardware, Microchannel and Parallel ports, Advanced Power Management, and support for ELF, aout, and other binary executables. For most new systems, the important details here will be the PCI options. Advanced administrators will probably want to pay close attention to the PCI options and the new sysctl interface.

# Networking Support

Unless you have a good technical reason (such as that you know what you're doing), you will need to include networking support. Many applications require this module on non-networked machines and will not run if this is not included. For the 2.2 kernel, you must also ensure that your net-tools package understands the new /proc/dev/net. net-tools-1.50 is also required to accommodate IPv6 protocol.

# BSD Accounting

BSD accounting is of most interest to ISPs and other organizations that need to track the use of their systems for billing or other accounting purposes. Adding BSD accounting will create a special file that logs and measures each process, allowing compatible software to gather detailed usage information.

# SysV IPC (DOSEMU)

Interprocess Communications (IPC) is a protocol for synchronizing and exchanging data between separate processes. If you plan on running the DOSEMU MS-DOS Emulator, you will need to include IPC. However, now that kmod has replaced kernelmod, there is no longer any need to include IPC in the main kernel. The 2.2 kernel now offers IPC as a loadable module, and removing kernelmod support from the IPC module has reduced its size by 40 percent.

# sysctl Support

Adding sysctl provides a means for controlling the running kernel either through system calls, or if the /proc filesystem is enabled, by writing to pseudo-files in the /proc/sys