+   cards and Universal Serial Bus (USB) flash drives. Such filesystems include TrueFFS, TFAT, FFS1, JFFS2, and YAFFS.

+   ■ The **RAM disk storage media**, which will be presented in Chapter 4, functions as a storage container by using a segment of main memory in RAM. The compressed ROM filesystem (cramfs) is used with many Linux distributions for initrd images (explained in Chapter 4).

+   ■ ***Special-purpose storage media*** are systems implemented to handle files, folders, metadata, and resuidals dynamically. Special-purpose filesystems are created by an application or software/system management tool. This includes database applications, registry-based applications, transactional-based systems, and various other unique file-based application systems.

The various Linux storage media types that are accessed can be accessed locally or remotely. Local storage media types, presented in the next section, are storage devices that are directly attached to your client machine. Remote storage media types, presented in the “**Network**” section, are filesystems accessed by your client machine through a network filesystem.

# Local

The local implementation of a filesystem is not uncommon. This approach alleviates many challenges that are typically associated with the implementation of network-based filesystems, RAM disk-based filesystems, and removable filesystems. This includes performance challenges due to limit network bandwidth, access failure due to lost network connectivity, redirection attacks that point your system to a different (perhaps compromised) server, and nonpersistent filesystems (for example, RAM disk) that require reconfiguration once the electrical power is restored.

In Chapter 2, several different local filesystems were introduced during the installation of the Linux system, including the three very common types (for example, ext2, ext3, and ReiserFS). Each filesystem has its own unique way of storing files and folders internally for quick access and indexing. This section will present some additional filesystems that are somewhat common. The filesystems are FAT, New Technology File System (NTFS), and Virtual File Allocation Table (VFAT).

FAT is a widely supported filesystem on most systems, and flash memory devices exist in many different standards. Those standards include FAT12, FAT16, FAT32, and a variation called VFAT. FAT12 has a cluster address limitation of 12-bits. It was designed to support storage devices with a maximum capacity of 16 MB (megabytes). FAT16, which has a cluster address size of 16-bits, was designed to support a maximum partition size of 2 GB