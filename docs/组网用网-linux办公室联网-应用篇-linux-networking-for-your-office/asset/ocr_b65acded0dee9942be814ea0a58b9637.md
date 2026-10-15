+   - Standard/generic (dumb) serial support—Select y or n here to use the serial ports on your motherboard, most plug-in one- or two-port serial boards, or an internal modem.
+   - Parallel printer support—Select y or m if you have a printer connected to the parallel port. You’ll also need to select y or m to Parallel port support in the General setup area.
+   - Mouse Support (not serial mice)—Select y here if you have a bus mouse or a PS/2 mouse.

# Mice

If you have a PS/2 mouse or a bus mouse, this area lets you enable drivers for specific types of mouse devices.

# Filesystems

One of the great advantages of Linux as a server is that it supports so many other operating systems’ filesystems. This isn’t very important for a server’s hard disks, but it can be for handling removable drives. If your network has mostly Windows computers except for a Linux server, you can read Macintosh 1.44MB floppies and removable disks on the Linux server, for instance. The filesystem options are split across the Filesystems, Network File Systems, Partition Types, and Native Language Support areas. Supported Linux filesystems and filesystem options include

+   - Quota support—You can limit the amount of disk space each individual user has if you select this option.
+   - Apple Macintosh filesystem support—This driver supports the Macintosh Hierarchical Filesystem (HFS) format, but not the more recent HFS+. Because HFS+ isn’t normally used on floppies or other removable media, this lack isn’t normally important.

# NOTE

> You can read Macintosh 1.44MB floppies on a PC, but not the older 800KB or 400KB floppies. These older floppies use a unique method of low-level encoding, and standard PC hardware can’t read that encoding. Apple switched to the same encoding scheme used by PCs with the Macintosh’s 1.44MB floppies, but kept HFS rather than the PC’s File Allocation Table (FAT) filesystem.