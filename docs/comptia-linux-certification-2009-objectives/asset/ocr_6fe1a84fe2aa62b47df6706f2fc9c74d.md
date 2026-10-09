![](bbox=[0.12, 0.09, 0.66, 0.4])

Figure 1-28: The different runlevels that can be specified with the telinit command.

# Init Runlevels Table

The following table describes the processes that can run at each init level.

| Init Level | Description |
| :--------- | :--------- | 
| 0 | Halts the system |
| 1 | Single-user mode |
| 2 | Multiuser mode without networking |
| 3 | Multiuser mode with networking |
| 4 | User configurable |
| 5 | Used for GUI (X11 multiuser mode) |
| 6 | Reboots the system |

# System Booting

During the installation of Linux, the *bootloader* you choose will be put on the **Master Boot Record** (*MBR*). GRand Unified Bootloader (**GRUB**) and Linux Loader (**LILO**) are the Linux bootloaders that load and start the kernel. Only one bootloader can be used on a system.

![](bbox=[0.77, 0.74, 0.88, 0.81])