
This method of managing kernel development can make selecting a kernel a confusing process. The important information to understand is how each kernel version is named, so you can choose the most appropriate options at a glance.

A kernel's name ends with a string of numbers in the format X.Y.Z. Each number is incremented as new features and bug fixes are added. X is the slowest to change; it could be years before there are kernels that begin with 3, for example. Deciding to change a major version number is a subjective act. Moving from a 2-based kernel to 3 would represent some kind of monumental advance. For example, when the version numbers jumped from 1 to 2, the following new items were added:

- Support for four new hardware architecture platforms (including Apple PowerPC and Atari)
- Additional IDE device drivers, better IDE error handling, autodetection of some IDE characteristics, and the ability to handle more controllers
- Additional SCSI device drivers
- Greatly expanded Ethernet card list
- The modern modular structure
- Advanced Power Management (APM) for devices such as laptop computers
- IP tunneling, masquerading, and additional routing capabilities
- ISDN support
- The VFAT and SMB file system support, among others
- File system quota support

Essentially, Linus Torvalds determines it is time to change the X kernel number when he feels that we are dealing with a brand-new starting point for kernel development.

The Y component changes on a semiregular basis, perhaps every six months or so. This is the crucial digit when determining whether the kernel is production or experimental. Experimental kernels have an odd-numbered Y component; for example, 2.3.12, 3.7.16, and 4.19.92. Production kernels, on the other hand, have an even-numbered Y component, such as 2.2.12, 3.8.16, or 4.20.92. The method for advancing this component is explained earlier in this section.

Perhaps the easiest to explain is the Z changes. Any time a change is made to the kernel code, the Z component advances. This method is used among most software developers. It is a way of knowing exactly what source code you are looking at. In fact, you may even see kernel versions in the format X.Y.Z-A. When you see this, you are looking at a version that was altered specifically for your Linux distribution.

For those who are more visually oriented, Figure 5.1 shows the full kernel development path and how the branches work out.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_158_0.png)

Figure 5.1 The kernel development stream.

## Kernel Documentation

The kernel source code comes with a set of documentation by default. Many of these files are useful for tracking down information about particular kernel modules or driver settings. What follows is a tour of the documentation directories so you know what is available and where to find it. To start looking for any kernel documentation file—if you already have the source code installed—go to /usr/src/linux/Documentation.

### General Kernel Files

Some of the documentation files are somewhat general. For example, the 00-INDEX file contains a list with one-line descriptions of all of the documentation files. This is useful if you download a version newer than the one that comes with Red Hat 6.2, because there may be subtle changes from what you see here. Another file is probably daunting for many, but some may be brave enough to tackle it. It is BUG-HUNTING, and contains instructions for how to track down and report a bug in the kernel. The ops-tracing.txt file contains additional information about this issue.

> **NOTE:** If you are interested in delving farther into kernel matters, a good place to start is “The Linux Kernel,” which is available at http://metalab.unc.edu/Linux/LDP/tik/tik.html, thanks to the Linux Documentation Project.

If you intend to write any code for the kernel, whether it is a bug fix or a patch to add a particular feature, be sure to read the CodingStyle file. This document is essentially a style guide for formatting kernel code. If you feel that this is infringing on your creativity, try to imagine what the kernel code would look like if the hundreds of people who have contributed code to the Linux kernel each used their own style conventions. Another important file in this regard is magic-number.txt, which lists the data structure magic numbers already in use.

For those who are interested in how the kernel handles input/output (I/O) mapping, take a look at the files IO-mapping.txt and ioctl-number.txt. If you like to run a wide range of binary file types and want to be able to do so from the command line, read the file binfmt_misc.txt. For Java-specific issues, read java.txt. You can also find out how the kernel deals with errors by reading the file exception.txt, and how it handles dependencies during configuration in smart-config.txt.

The kernel-parameters.txt file contains the parameters accepted by the kernel at boot time. Also, there is a document that explains the workings of the program that manages kernel modules. This file is lkmod.txt. Another deals with background information about the Linux kernel’s ability to dynamically load and unload modules: modules.txt. To see how the kernel handles file locking, read the file locks.txt and the related background information file mandatory.txt. Memory issues are covered in memory.txt.

Pointers to a wide range of kernel documentation are available in the file kernel-docs.txt.

### Architecture-Specific Files

There are some files among the kernel documentation that specifically deal with one form of hardware architecture or another. These files are:

- **ARM-README**—Notes from the ARM code development team regarding specific issues ARM users need to consider.
- **IO-APIC.txt**—Useful for those who have Intel or Intel architecture-based SMP-capable motherboards. Not all motherboards are completely IO-APIC compliant. This file discusses how to tell if your motherboard is compliant, and how to deal with problems.
- **arm**—This subdirectory contains additional files relating to the ARM version of Linux.
- **i386**—This subdirectory contains additional files relating to the i386 (Intel) version of Linux.
- **m68k**—This subdirectory contains additional files relating to the Macintosh 68k version of Linux.
- **mca.txt**—Discussion of i386 Microchannel architecture handling under Linux.
- **mtrr.txt**—Discussion of Memory Type Range Control on Intel Pentium Pro and Pentium II systems.
- **powerpc**—This subdirectory contains additional files relating to the Macintosh PowerPC version of Linux.
- **sgi-visws.txt**—Discussion of Linux handling of SGI Visual Workstations.

### Hardware-Specific Files

There is a small difference between architecture-specific and hardware-specific files: Architecture refers to the overall type of system design; hardware is more a device label than a design label. The files among the kernel sources that are related to specific devices are:

- **README.DAC960**—Information specific to the Mylex DAC960/DAC1100 PCI RAID Controller.
- **cdrom**—This subdirectory contains information files on a number of CD-ROM models and manufacturers.
- **comptone.txt**—Information specific to the Comptone Intelliport II/Plus Multiport serial driver.
- *epgarray.txt*—Information specific to Compaq's SMART2 Intelligent Disk Array controllers.
- *digiboard.txt*—Information specific to the Digiboard PC/Xi, PC/Xe, and PC/Xeve multi-modem hardware.
- *digiecpa.txt*—More information pertaining to Digiboard technology.
- *fb*—This subdirectory contains information files on frame buffer drivers and devices. Frame buffering is related to how your machine handles graphics.
- *filesystems*—This subdirectory contains information files on the various file system types that Linux understands.
- *ftape.txt*—Discussion regarding the ftape tape driver.
- *hayes-esp.txt*—Information specific to Hayes ESP (Enhanced Serial Port) modems.
- *ide.txt*—Information regarding the Linux kernel's handling of IDE devices.
- *isdn*—This subdirectory contains information about the kernel's ISDN handling and the various drivers available, including information about PPP over ISDN.
- *joystick-api.txt*—Information on writing code that utilizes Linux's joystick capabilities.
- *joystick-parport.txt*—Information on Linux and parallel port joysticks.
- *joystick.txt*—Information on Linux joystick drivers.
- *md.txt*—Discussion of Linux Multi Disk device handling.
- *mkdev-ida*—This is actually a shell script that helps you to set up device information for SMART RAID IDA controllers.
- *networking*—This subdirectory contains information on the various network card device drivers available in Linux.
- *paride.txt*—Discussion of Linux and IDE parallel port devices.
- *parport.txt*—Discussion of Linux parallel port support and modules.
- *pci.txt*—Discussion of what to avoid when writing PCI drivers.
- *pcwd-watchdog.txt*—Discussion of how Linux handles the ISA Berkshire PC Watchdog card.
- *ramdisk.txt*—This file is not really hardware-specific, but it does involve a driver: the RAMdisk driver used in Linux.
- *riscom8.txt*—Notes about the RISCcom/8 multiport serial driver.
- *rtc.txt*—Discussion about the realtime clock driver used in Linux to go along with the PC and Alpha architectures.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_161_0.png)
