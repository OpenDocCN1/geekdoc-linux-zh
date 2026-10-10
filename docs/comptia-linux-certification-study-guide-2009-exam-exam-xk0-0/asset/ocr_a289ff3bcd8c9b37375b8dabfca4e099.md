**Table 4.1 Dual Roles of init Command**

| Existing Linux init Role | New Installation init Role |
| :--- | :--- |
| 1. Loading the source containing the Linux distribution installation medium for installation | 1. System drivers loading for Linux kernel |
| 2. Hardware scanning and selecting of hardware drivers | 2. Creating special system files for the kernel |
| 3. Loading the installation system or rescue system | 3. Managing redundant array of inexpensive disks (RAID) and Logical Volume Manager (LVM) setups |
| 4. Linux installation package and system configuration tool | 4. Managing network configuration |

the loading of modules and instructions to implement all operating system services [for example, process management, concurrency, and memory management]. The Linux kernel integrates the CPU architecture through a series of device drivers and kernel extensions. The init program will perform one of two different options, as shown in Table 4.1. The first option is the execution of a preinstalled (existing) copy of the Linux operating system. The second option is for a new installation of the Linux operating system.

More details about the `init` command will be provided later in the “Installing GRUB and Booting Linux” section. Regardless of which approach init takes, the init program mounts a mass storage device to obtain access to the root filesystem. Before granting access, the init program performs error checking. After the error checking process, the init program removes the virtual disk file system (initrd) from the memory.

The fourth stage, “loading the root filesystem,” is the final stage. During this stage, the Linux kernel will use the init program to load and grant access to the actual root filesystem. This entails making sure the Linux kernel has access to the necessary hardware device drivers and the execution of any specific instructions for starting the Linux operating system (known as *run-levels*). More details about runlevels will be provided later in the “Runlevels” section. To perform this task, while making sure the Linux kernel has access, the original init program will execute a new init program that resides on a mounted hard drive. This new “`init`” program will load the Linux Login screen, as shown in Figure 4.2.

The four stages provide an overview of the Linux booting process for the Linux+ certified professional. The remaining focus of the chapter is on GRUB, runlevels, and troubleshooting boot issues.