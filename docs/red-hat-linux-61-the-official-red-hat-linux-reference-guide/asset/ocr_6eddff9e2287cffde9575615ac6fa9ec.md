# Chapter 1. Boot Process, Init, Shutdown

3

Once the second stage boot loader determines which kernel to boot, it locates the kernel binary in the /boot/ directory. The kernel binary is named using the following format — /boot/vmlinuz-<kernel-version> file (where <kernel-version> corresponds to the kernel version specified in the boot loader settings).

For instructions on using the boot loader to supply command line arguments to the kernel, see Chapter 2 Boot Loaders. For information on changing the runtime at the GRUB or LILO prompt, see Section 2.10 Changing Runtimes at Boot Time.

The boot loader places the appropriate initial RAM disk, called an initrd, into memory. The initrd is used by the kernel to load drivers necessary to boot the system. This is particularly important if SCSI hard drives are present or if the systems use the ext3 file system.

> Warning
Do not remove the /initrd/ directory from the file system for any reason. Removing this directory will cause the system to fail with a kernel panic error message at boot.

Once the kernel and the initrd image are loaded into memory, the boot loader hands control of the boot process to the kernel.
For a more detailed overview of GRUB and LILO boot loaders, see Chapter 2 Boot Loaders.

# 1.2.2.1. Boot Loaders for Other Architectures

Once the Red Hat Linux kernel loads and hands off the boot process to the init command, the same sequence of events occurs on every architecture. So the main difference between each architecture's boot process is in the application used to find and load the kernel.

For example, the Alpha architecture uses the aboot boot loader, while the Itanium architecture uses the ELILO boot loader.

Consult the Red Hat Linux Installation Guide specific to these platforms for information on configuring their boot loaders.

# 1.2.3. The Kernel

When the kernel is loaded, it immediately initializes and configures the computer's memory and configures the various hardware attached to the system, including all processors, I/O subsystems, and storage devices. It looks for the compressed initrd image in a predetermined location in memory, decompresses it, mounts it, and loads all necessary drivers. It initializes virtual devices related to the file system, such as LVM or RAID before mounting the initrd disk image and freeing up all disk memory once occupied.

The kernel then creates a root device, mounts the root partition read-only, and frees any unused memory.

At this point, the kernel is loaded into memory and operational. However, since there are no user applications that allow meaningful input to the system, much can be done with it.

In order to set up the user environment, the kernel executes the /sbin/init program.

2. For details on making an initrd, see the chapter titled The ext3 File System in the Red Hat Linux Customization Guide.