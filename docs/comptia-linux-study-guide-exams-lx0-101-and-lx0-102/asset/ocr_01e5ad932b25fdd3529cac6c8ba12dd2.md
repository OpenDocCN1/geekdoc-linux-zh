Timeout The timeout= option defines how long, in seconds, to wait for user input before booting the default operating system.

Background Graphic The splashimage points to a graphics file that's displayed as the background for the boot process. This is optional, but most Linux distributions point to an image to spruce up the boot menu. The filename is relative to the GRUB root partition, if /boot is on a partition, portion of the path is omitted. Alternatively, the path may begin with a GRUB device specification, such as (hd0,5) to refer to a file on that partition.

# Essential GRUB Legacy Per-image Options

GRUB Legacy's per-image options are often indented after the first line, but this is a convention, not a requirement for identification and continue with options that tell GRUB to handle the image:

The title line defines a per-image stanza and the label to display when the boot loader. The GRUB title can accept spaces and is conventionally descriptive, as shown in Listing 5.1.

GRUB Root The root option specifies the location of Legacy's root partition. This /boot partition if a separate one; otherwise, it's the Linux root (/) partition. GRUB can reside on a FAT partition, on a floppy disk, or on other OS' partitions, though, GRUB

Kernel Specification The kernel option describes the location of the kernel as well as any kernel options that are to be passed. Paths are relative to GRUB Legacy's root partition. As an alternative, you can specify devices using GRUB's syntax, such as kernel(hd0,5)/vmlinuz root=/dev/sda. Note that you may pass more kernel options on this line. Some boot loaders split off kernel options on separate lines; but in GRUB, you incorporate these options into the kernel line. The root option specifies the kernel to mount its filesystem read-only (it's later mounted read/write), and the root+ option specifies the Linux filesystem. Because these options are passed to the kernel, they use Linux-style device identifiers, unless other options in the GRUB configuration file.

Initial RAM Disk The initrd option to specify an initial RAM disk, which holds a minimal set of drivers, utilities, and configuration files that the kernel uses to mount its root filesystem before the kernel can access the hard disk. Most Linux distributions heavily on the initial RAM disk as to keep the kernel file small and to provide tools to the kernel in the boot process before they could be loaded from the hard disk.

Non-Legacy The rootify option is similar to the root option except that GRUB Legacy won't try to access files on this partition. It's used to specify a boot partition for OSs for which GRUB Legacy can't directly load a kernel, such as DOS and Windows.

Chainloading The chainloader option tells GRUB Legacy to pass control to another boot loader. Typically, it's a +1 option to load the first sector of the target OS's root partition (usually specified with rootnofify) and to hand over execution to this secondary loader.