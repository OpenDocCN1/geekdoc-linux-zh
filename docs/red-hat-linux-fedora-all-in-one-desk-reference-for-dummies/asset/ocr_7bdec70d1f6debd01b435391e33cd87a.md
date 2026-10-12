on these devices, consult the documentation in the /usr/src/linux*/Documentation/video4linux directory.

# File systems

Through this category of options (shown in Figure 6-14), you can turn on support for specific types of file systems. You’d be amazed by the many different file systems that the Linux kernel can support. Table 6-1 lists some of the file systems that Linux can support. You would typically build a kernel with support for the core Linux file systems (ext2 and ext3), CD-ROM file system (ISO 9660 and Joliet), and DOS/Windows file systems (MSDOS, FAT, and VFAT).

![](bbox=[0.25, 0.45, 0.75, 0.82])

Figure 6-14: Turn on support for specific file systems from this configuration window.

Table 6-1 Some File Systems Supported by Linux Kernel

| File System | Description |
|---|---|
| Apple Macintosh | The Macintosh HFS file system (Linux can read and write Macintosh-formatted floppy disks and hard drives). |
| Coda | An advanced network file system that is similar to NFS but that better supports disconnected operation (for example, laptops) and is a better security model. |
| Ext2 | The second extended file system — the current standard file system for Linux. |

(continued)