
also in flash EPROMs) contains a series of functions, the so-called BIOS
interrupts, for example 0x10 for screen control or 0x13 for diskette and hard
disk access. This means that minor deviations in hardware control can be
adjusted by means of corresponding adaptations of the BIOS – this was one of
the reasons for the use of IBM-compatible PCs.

Any expansion board or component designed to be IBM-compatible must
react to appropriate calls, for example initialization by the BIOS, in a well-defined manner. This created a certain independence from specific peripheral
devices, which contributed substantially to the development of the market for
IBM-compatible components. To be accurate, the compatibility is with Intel,
more precisely with the Intel 8088/86 processor, since the software burnt into the
BIOS chips consists of instructions for this processor.

There is a multitude of BIOS versions, practically one for each type of
motherboard. How individual functions are implemented and in which order
are processed, to a certain extent, the benefit of the manufacturer.
The following overview of a BIOS start-up should therefore be only as an
example.

After switching the power on, the BIOS is, via hardware, loaded into the
memory area from 0xF000 to 0xF000:FFFF, and the program counter
is set to the address 0xF000:FF00, which starts the execution of the BIOS
codes. The processor starts in the real mode, then the memory only 1
Mbyte is available. Usually, the BIOS only contains code for this mode, so
it cannot be used by protected-mode systems such as Linux.

Before the BIOS begins to test itself and the computer's periphery, it checks
the memory area between the graphics adapter on address 0xA000 and its starting address for BIOS extensions of other plug-in boards, for example
network cards. Cards with their own BIOS are recognized from the BIOS
signature 0xAA55 or 0x55AA at the end of a 32k block.

The BIOS then executes the 'Power On Self Test' (POST): the functions of
the processor itself, the registers, and several commands are checked; if the
processor is defective, the PC is halted without displaying a message. With
errors, some BIOS versions produce acoustic signals, according to
the beeps, provide information on the nature of the error. Then,
checksums are made over the ROM itself and compared with the stored values to
detect possible defects in the ROM BIOS or, if this is already copied into RAM,
in the corresponding RAM component.

Subsequently, further components of the motherboard, such as interrupt and
DMA controllers and main memory, are tested and initialized. The POST
continues with checks of keyboard, diskette, and hard disk drives. The results of
this test are stored in BIOS variables, and the interrupt vector table is initialized.

# THE BASIC INPUT/OUTPUT SYSTEM (BIOS) 45

By means of the BIOS interrupt 0x19, the boot process itself is initiated or the 'bootstrap loader' is called.

The early initialization of the extension cards makes it possible for a network card to take over the function of the boot loader during the boot process. This function is used if one wants to boot a computer via a network. This has several advantages:

- Even when the computer is switched off, you can carry out configuration adaptations on the boot server.
- The computer needs no hard disk or only a small one for swapping. This makes it very quiet.
- A computer can be reconfigured relatively easily, for example with a new IP address or a new kernel.

Obviously this function has some disadvantages: the network load increases and some accesses are slower than NFS than on a local hard disk. If you wish to use this function, you can find additional documentation in the file Documentation/nfs-root.txt in the kernel sources and in the Mini-HowTos NFS-root and NFS-Root-client.

# 3.1.1 Loading from floppy disk or hard disk

In a sequence which is the same for all operating systems, attempts are made to read the first sector of /dev/fd0 (drive A:) and then of /dev/hda (drive C:). More recent BIOS versions allow a different order to be specified via a setup; this first changed order is stored in the CMOS RAM. With floppy disks, this first sector is called the boot sector sector; with hard disks, it is called the Master Boot Record (MBR). The size is always 512 bytes. You can only boot from SCSI disks if no IDE disks are installed in the system or if the BIOS supports this function even with IDE disks.

Many UNIX workstations can also be booted from tape or from CD; these functions too are only implemented in more recent PC BIOS versions or in the BIOS of the SCSI controller. If your BIOS supports this function, you can boot directly from a LINUX CD and install the system - without diskettes.

# 46 SYSTEM START-UP

| 0x000 | |
| :--- | :--- |
| Offset: 0x000 | Program code |
| 0x1BE | Partition table |
| 0x1FE | Magic Number (0xAA55) |

**Figure 3.1** Structure of a Master Boot Record.

The MBR (see Figure 3.1) of a hard disk contains four entries of 16 bytes each, that is one for each of the four possible (primary) partitions. up to a primary partition is further subdivided, it is called an extended partition; up to four-logical drives can be created per (extended) partition; that is, you can have a maximum of logical drives per partition.

Besides specifications regarding the type of partition (for example Linux = 83, Swap = 82) and start, end, and size of the partition, each of the MBR also contains a flag which indicates whether the partition is 'active' and therefore used. The program code located before the partition table de-facto loads the boot sector. Independently of the operating system, a boot loader has the task of determining the active partition and loading the boot sector by making use of BIOS routines. In the beginning, there were only primary partitions under MS-DOS. Modern boot loaders under LINUX, in contrast, offer many more options; you can also boot from logical drives

# THE LINUX BOOTADER 47

| MBR | Boot sector | Operating system |
| :--- | :--- | :--- |
| DOS-MBR | Boot sector | IO.SYS, MSDOS.SYS |

Recent LINUX versions are so large that they can no longer be loaded into the first megabyte of memory. Possible solutions are kernel modules or the generation of bImage which is already loaded in protected mode.

# 3.2 The boot loader

In contrast to the MS-DOS, modern boot loaders such as LILO under LINUX offer many more possibilities; for example, booting of other operating systems, changing between different versions of an operating system, and passing of parameters at the start of the kernel.

The three most important boot loaders for LINUX are: LILO, loadlin, syslinux. All three of the above boot loaders share the capability for accepting parameters or arguments passed ‘by hand’ at the call or at a point of time during loading. These parameters affect both the boot loader itself, the kernel or the init process, or they are stored as environment variables and can be used for the configuration of process.

The parameters for the boot loader itself contain information such as the name and path of the kernel file to be loaded and an indication of the partition which it can be found. All parameters that the boot loaders do not understand are simply passed to the kernel; the kernel itself or a device driver will evaluate them and, if needed, configure hardware. The kernel in turn passes the parameters it does not know, or those it recognizes but does not process, to init. The values that even init do not recognize are stored as environment variables in the format variable=value and can thus be evaluated by a shell or any other program.

This flexibility of the various programs involved in handling the boot parameters, however, also has the consequence that options are not only passed but sometimes overwritten. This is, for example, intentional when values hard compiled into the kernel, such as the interrupt or port of a network card, turn out to be incorrect at a later stage.
