Red Hat Linux also supports a variety of partition types, including MS-DOS, VFAT, HPFS, and NTFS, the standard Red Hat Linux kernel cannot access the HPFS and NTFS file systems; you must recompile the kernel if you require this support.

The Linux kernel supports a swap partition as large as 2GB. Up to eight swap partitions can be defined.

# Mount Points

Like UNIX, Linux mounts partitions of block devices as subdirectories within a unified system. The directory that holds the contents of a partition is called its mount point. The following two partitions, known by their mount points, are particularly important:

+   * The root file system

+   /boot The boot partition, which contains the Linux kernel

The root partition is mounted at the beginning of the system initialization process, after the kernel itself has been loaded into memory. Its identity must be known to the kernel and is typically passed to the kernel by the L11o bootloader on Red Hat Linux systems. Other partitions are integrated into the system by being mounted as subdirectories of the root file system.

The boot partition is a small partition used to circumvent the 1024-cylinder restriction affecting the BIOS of many systems. By locating the boot partition within the first 1024 cylinders, the Linux kernel is guaranteed to be available to the BIOS.

# Summary

In this chapter, you learned about Linux support for a wide variety of hardware devices. The following are the most important topics covered in this chapter:

+   **Hardware Compatibility** Red Hat, Inc. publishes a list of hardware that is compatible with and supported by Red Hat Linux.

+   **Hardware Configuration** A hardware device must generally be assigned a unique IRQ and base I/O address. Some devices must also be assigned a unique DMA.

+   **Adapter Cards** Configuring PCI adapter cards is straightforward. Configuring other types of cards, especially ISA plug-and-play cards, can be more difficult.