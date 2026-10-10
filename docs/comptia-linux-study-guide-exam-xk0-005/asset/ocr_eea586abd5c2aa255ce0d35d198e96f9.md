The PXE **LINUX** bootloader uses the *Pre-boot eXecution Environment (PXE)* standard, which defines how a network workstation can boot and load an operating system from a central network server. PXE uses DHCP to assign a network address to the workstation and BOOTP to load the bootloader image from the server. The network server must support the TFTP protocol to transfer the boot image file to the workstation.

To utilize **PXE LINUX**, the TFTP server needs to have the **PXE LINUX** bootloader program, stored as `/tftpboot/pxelinux.0`, available for the workstations to download. Each workstation must also have a configuration file available in the `/tftpboot/pxelinux.cfg` directory. The files are named based on the MAC address of the workstation and contain specific configuration settings required for that workstation.

![](bbox=[0.12, 0.33, 0.22, 0.41])

> Although PXE was designed to use TFTP to load the boot image, it has been modified to also load the bootloader image stored on a netwrok server using NFS, HTTP, or even FTP.

# # System Recovbery

There’s nothing worse than starting up your Linux system and not getting a login prompt. Plenty of things can go wrong in the Linux startup process, but most issues come down to two categories:

+   - Kernel failures
+   - Drive failures

The following sections walk through some standard troubleshooting practices you can follow to attemp to recover a Linux system that fails to boot.

# ## Kernel Failures

Kernel failures are when the Linux kernel stops running in memory, causing the Linux system to crash. This is commonly referred to as a *kernel panic*. Kernel panics often are a result of a software change, such as installing a new kernel without the appropriate module or library changes or starting (or stopping) a program at a new runlevel. Often these types of boot errors can be fixed by starting the system using an alternative method and editing the necesary files to change the system.

# ## Selecting Previous Kernels at Boot

One of the biggest culprits to a failed boot is when you upgrade the Linux kernel, either on your own or from a packaged distribution upgrade. When you install a new kernel file, it’s always a good idea to leave the old kernel file in place and create an additional entry in the GRUB boot menu to point to the new kernel.