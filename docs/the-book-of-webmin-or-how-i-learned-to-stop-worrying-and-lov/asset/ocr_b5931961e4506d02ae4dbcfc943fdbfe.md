![](bbox=[0.25, 0.15, 0.75, 0.38])

Figure 14-6: Edit boot option

# Boot image partition

This option allows you to specify the location of the item to be booted. It is not required to be on the same disk or partition as the GRUB boot loader, but it must be contained on a disk and filesystem type that GRUB is able to access. This option corresponds to the root directive.

# Operating system to boot

Here you may specify the type of operating system to boot and the filename of the specific kernel to boot if booting a Linux kernel. GRUB supports most operating systems that have their own boot loader, in addition to booting Linux directly. Thus, it is possible to boot Windows operating systems, multiple Linux versions, or BSD operating systems, using the same GRUB menu. Kernel options may be passed to a Linux kernel, by specifying them in the kernel options field of this section. For example, you may wish to have a menu item entitled Single User that boots your system into single user mode, for emergency maintenance (or resetting the root password, if it is lost). Doing this simply requires you to copy an existing boot entry and add the word single to the end of the list of existing kernel options.

# Password locked?

GRUB has relatively fine-grained access control (for a boot loader, anyway), in that you can specify which boot menu items will require a password to boot. This option corresponds to the lock directive. Password protection must be enabled in the Global Options page for this directive to work.

# Partition Manager

The partition manager provides a graphical interface to both the fdisk partition editing command and the /etc/fstab file on your system (Figure 14-7). fdisk is commonly used to create and remove partitions on a disk, while /etc/fstab file is where the mounting information for the system is configured.