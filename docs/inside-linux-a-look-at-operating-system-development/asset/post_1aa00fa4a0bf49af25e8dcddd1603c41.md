
to jump the cursor to a place on the screen other than the next position. There exists an ANSI³ standard describing the control sequences which should be sent for various effects. The DEC VT100 and its successors offer the ubiquitous example of this feature in a terminal, but when the system display screen is used, the kernel must provide this capability.

## 7.3 File Management

Linux does not impose structure on its files. Any such structure is supported only through run-time libraries and application code.

We have seen a few cases where the operating system kernel “peeks” inside a file:

- it looks at the magic word of an executable to determine how the file is to be executed or interpreted,
- it can develop a file system inside a file using some experimental modules, and
- it can support compressed and encrypted files using other experimental modules.

### 7.3.1 Database

Database implementations require some kind of mechanism to ensure mutually exclusive access to records. Some kernels offer record locking, but Linux does not. Instead, Linux offers semaphore operations from which any kind of mutual exclusion system can be built.

### 7.3.2 Version Control

Some file systems have a built-in mechanism to track file versions. The FILES-11 used in RSX-11 and VMS and the file system used by Tenex and TOPS-20 have provisions for a version number as part of a file’s fully qualified name. If a file was opened without reference to a version number, the most recent version was used. When a file was created or written, the file took on the next version number. When a file was deleted, the oldest version was deleted.

Linux has no such mechanism. Utilities such as SCCS (Source Code Control System), RCS (Revision Control System), and CVS (Concurrent Versions System) are used to manage revision history explicitly. Their use has been integrated into other tools such as make.

### 7.3.3 Archive/Backup

Although these operations are mentioned together, they are distinct in purpose and therefore operation. The difference is somewhat philosophical—archive is intended for long-term holding of files which are rarely referenced and backup offers day-to-day convenience in restoring lost files.

Therefore, archive operations often focus on compression and stability and backup operations focus on convenience.

Some utilities directly access the disk and rely on their understanding of the file system implementation. This direct access yields greater performance at the cost of portability.

The system kernel issues are:

- what special file types exist?
- can ownership, access, timestamp, and other characteristics be restored exactly?
- can the backup device (usually tape) be operated at full performance?

## Chapter 8 Hardware

Previous chapters have looked at memory management, emulation of floating point arithmetic, and some higher level aspects of peripheral control. This chapter is intended to explore some more of the issues in coupling the system kernel to the hardware.

### 8.0.4 Some More Historical Background

The goal of the operating system is to ease the programmer's burden. It must hide the details of device programming, it must protect users from one another (and from their own mistakes), and it must equitably manage system resources.

At one time, these goals were compromised on personal computers because of limited resources (and perhaps because of the shortsightedness of the designers).

Hardware performance has been growing exponentially for many decades. (Moore's Law notes that it doubles every 1.5 years.) This improvement has caused us to constantly revise our approaches to problems. For instance, it has been noted earlier that bit-mapped displays weren't practical until memory prices fell low enough. The decreasing cost of memory also means that programming styles have shifted from “do it with as little memory as possible” to “make sure it's correct and easy to understand”. Processors can easily handle communication transfer rates which would choke the first 8086 system. This means that we can use these new systems for demanding applications such as file system servers and multi-user timeshare systems.

In some cases the system hardware has not advanced as quickly as the central processor. For instance, the IBM personal computer was designed for less than 1 Mbyte of memory at a time when no individual was likely to buy that much memory. This led to a decision to use locations above 640 Kbytes to address peripheral devices. Following this decision by IBM, Microsoft Corporation released an operating system which relied on an addressing mode which was normally limited to a 1 Mbyte address range.

Now that personal computer systems are commonly sold with 8 Mbytes of memory, the earlier decision looks foolish.

Fortunately this decision can be overcome through the appropriate use of memory mapping. In the case of MS-DOS, this memory mapping is still unwieldy because of a desire to maintain compatibility with old systems. Linux suffers less because it requires one of the later model Intel computers and it uses a convenient memory addressing scheme.

In a similar vein, the bus used to access peripherals was initially quite narrow (8 bits) and slow (5-10 MHz). Since then, improved buses have been designed to provide paths which are wider (32-64 bits) and faster (33 MHz).

### 8.1 Selection and Performance

The personal computer market has spawned an amazing number of different peripherals, some of which barely satisfy the bus standards and a few which don't quite meet the bus standards.

Because of its preeminent market position, MS-DOS does not have to directly support all these different peripherals. Peripheral manufacturers provide drivers for their devices in a ROM on the control card. The Basic Input/Output System incorporates these drivers as part of its interface to MS-DOS and to stand-alone programs. (We saw in Section 5.7.3 how these drivers are used by the Linux Loader (LILO).)

Although newer peripherals have correspondingly newer ROMs, the basic BIOS interface remains somewhat limited. For instance, it cannot directly address disk tracks beyond 1023 and it does not support multi-tasking use of peripherals because the subroutines are not re-entrant.

Therefore, Linux is obliged to incorporate support for all these different peripherals. This support is not as restricted as it once was. Some hardware manufacturers are providing Linux drivers and where this does not happen, volunteers can often modify an existing driver from a similar peripheral.

The Hardware HOWTO lists devices which have known support, devices which have limited support, and devices which are known to have no support. The list of supported devices is growing towards the time when *all* devices will be supported.

The following subsections outline some of the issues which must be considered when selecting hardware for a Linux system. They are not intended to summarize the HOWTO.

#### 8.1.1 Memory

- **30 pin** supports 256K×9, 1M×9, or 4M×9 SIMMs (Single Inline Memory Module).
- **72 pin** supports ×32 or ×36 (4 bytes with or without parity) SIMMs. Because the greater width generally leads to higher performance, this form is common in newer and high-end systems.

#### 8.1.2 Bus

- **ISA** This bus is 8–16 bits wide and operates at 8.33 MHz (but nonstandard to 12.5 MHz). This is the “universal” standard.
- **EISA** This bus is 32 bits wide and operates at 8.33 MHz. This design also supports ISA peripherals.
- **VESA local bus** This bus is 32 bits wide and operates at 40–50 MHz. The development of this bus design was driven by needs of video controllers, but some storage interfaces also use this bus.
- **Micro Channel Architecture** This bus was developed by IBM to solve problems with other bus designs. Although a good design, its popularity has been hindered by licensing restrictions. It is not well supported by Linux.
