# CREATING LINUX PARTITIONS 35

When we talk DOS, we actually include all operating systems build on DOS, in particular Windows 3.1 and the first version of Windows 95. Not affected, with regard to hard disk, are Windows 95b, Windows 98, Windows NT, and the future Windows 2000. These operating systems access the hard disk in a similar way to Linux. However, as with Linux, there are problems with the start-up of the operating system if it is installed beyond the 1024-cylinder barrier.

For real data access, many BIOS versions distinguish between XCHS and LBA mode (logical block addressing). In the first case, the new (fictitious) CHS geometry is used and the BIOS converts the values into the CHS geometry of the disk. In the second case, the sectors are simply numbered sequentially. The BIOS handles the LBA number directly over the disk and thus saves a conversion step. (This obviously presumes that the disk understands LBA values; with modern IDE disks, this is the case.)

# Disk managers

The second variation is less elegant than the BIOS solution and has fortunately become less customary; instead of a more program BIOS, a so-called disk manager is used. This is a small program which is activated immediately after starting the computer and performs a CHS conversion similar to the BIOS.

Disk managers are unavoidable if the full capacity of a new IDE disk is to be exploited with an old IDE controller under DOS. Disk managers do not happily coexist with Linux. Try to avoid installing them from the very beginning!

# Disk access under Linux

Now to Linux: as Linux does not use the BIOS when it is running, there is no 1024-cylinder limit and therefore no disk size limit. Within Linux, disk access is not carried out CHS, but through logical block addressing (LBA). Two sectors are combined into a block (1024 bytes), and all blocks are numbered sequentially.

Nevertheless, the inadequacies of DOS and the BIOS create problems even for Linux, with two reasons:

+   - On the other hand, at Linux the boot kernel is supposed to be loaded from the hard disk.(Theoretically, it is also possible to write the kernel to a disk and read it there—however, this is slower and not particularly elegant). The Linux loader (in short, LILO) is responsible for the start-up, and the loader has to run on the BIOS. Therefore, in order to be able to start Linux from the hard disk, the kernel must lie within the first 1024 cylinders. (As already stated: with modern hardware, the 1024-cylinder limit corresponds to 7.9 Gbytes. The ancient rule that the kernel must be located within the first 504 Mbytes applies only hand, to very old hardware.)

+   - On the other hand, it is desirable that disk access is carried out following the same scheme under DOS and under Linux. In particular, all operating systems

![](bbox=[0.065, 0.735, 0.153, 0.988])