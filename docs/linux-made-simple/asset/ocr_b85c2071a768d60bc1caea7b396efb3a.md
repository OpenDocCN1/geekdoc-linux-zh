# Boot sequence

The mysterious sequence of flashes and beeps at startup.

Most distros go straight to a splash screen when booting, so we don’t see what is happening. In fact, there’s a lot going on both before the splash screen appears and then hidden by the screen. The BIOS starts up first, in the motherboard’s hardware. It looks for a boot device and loads code from there.

In the case of a hard drive using the traditional DOS partition system, this is contained in the Master Boot Record (MBR) of the drive – just 512 bytes of storage. 64 bytes are used to hold the partition table for the drive (which is why only four primary partitions are available), leaving all of 446 bytes for the bootloader code, usually Grub. 446 bytes doesn’t give room for much in the way of features, so all this code does is load the rest of the boot code from elsewhere on the disk, from a location set when the MBR code was installed by the bootloader.

The bootloader reads its configuration file, usually /boot/grub2/grub.cfg, for a list of boot options, and either displays a menu or goes straight to the default boot. Linux is not involved at this point, because there is only the bootloader code running.

file it may need, plus other settings such as the root partition, and whether to hide all this behind a splash screen. If you want to see what happens from here on, you can disable the splash screen on most distros by pressing the [E] key to edit the Grub menu entry, removing any quiet and splash options and pressing [F10] to continue booting.

# Why use a ramdisk?

Most distros use an initramfs file. The main reason for this is that certain drivers have to be loaded with the kernel, particularly those needed to load anything for the disk drive (like SATA controllers and filesystem code). For a generic distro, building all possible options into the kernel would make it unworkably large, so everything is built as modules and those needed for booting are included in the initramfs. This is a type of ramdisk that is loaded with the kernel by the bootloader (using the BIOS routines to read it from the disk) containing all the files needed to mount the root partition. This is done using the kernel’s device detection to decide which to load, and then control is passed to the hard disk proper. The initramfs is also used to load any splash screens, so they appear right at the start of the boot process.

> “The config file tells the bootloader the location of the Linux kernel”

Removing the boot splash screen shows the boot process in its entirety, including the status of the services being started.

![](bbox=[0.23, 0.53, 0.565, 0.7])

Once the root partition is mounted, directly or via the initramfs, the init sequence starts in earnest. Traditionally, this involves running /sbin/init, which then runs everything else, as controlled by /etc/inittab, and is responsible for the list of service start-up messages you see scrolling up the console if you have no splash screen. This also allows you to see where the boot process is hanging or taking an unreasonable time if you experience such problems.

# Newer options

Time moves on, and all of these systems are subject to change. On the latest hardware, the BIOS has been replaced by UEFI, although once the bootloader is installed you won’t

# The GNU of GNU/Linux

The GNU (Gnu’s not Unix) project predates Linux by several years. It had created most of the basic tools needed by a computer of the early 1980s – compilers, text editors, file and directory manipulation commands and much more – but did not have a usable kernel (some would say their kernel, GNU Hurd, is still not that usable). When Linus Torvalds started tinkering with his small project in 1991, he had a kernel without the tools to run on it.

The two were put together and GNU/Linux was born – an operating system using the Linux kernel and the GNU toolset. It is not only the programs in /bin and /usr/bin that come from GNU; glibc is the core C library used in Linux and it also comes from GNU. So just about any time you do anything on your computer, every time you type a command or click an icon, GNU software is being run at some level.

No wonder the GNU die-hards get upset when we refer to our operating system as Linux and not GNU/Linux. It is worth mentioning that no one really denies the importance of the GNU aspect; calling the OS Linux rather than GNU/Linux has far more to do with convenience and laziness than politics – the full title is just too cumbersome.

![](bbox=[0.7, 0.76, 0.9, 0.88])

Sorry Richard, we can’t be bothered to say ‘GNU slash’ every time.