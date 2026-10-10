Firmware Interface) standard, was created.

GPT-partitioned disks can be used either with computers with the traditional PC BIOS or ones with UEFI firmware. On machines with a BIOS, the second part of GRUB is stored in a special BIOS boot partition.

On systems with UEFI firmware, GRUB is loaded by the firmware from the files grubia32.efi (for 32-Bit systems) or grubx64.efi (for 64-Bit systems) from a partition called the ESP (EFI System Partition).

# The /boot Partition

On Linux the files necessary for the boot process are usually stored on a boot partition, mounted under the root file system and colloquially referred to as /boot.

A boot partition is not needed on current systems, as boot loaders such as GRUB can usually mount the root file system and look for the needed files inside a /boot directory, but it is good practice as it separates the files needed for the boot process from the rest of the filesystem.

This partition is usually the first one on the disk. This is because the original IBM PC BIOS addressed disks using Cylinders, Heads and Sectors (CHS), with a maximum of 1024 cylinders, 256 heads and 63 sectors, resulting in a maximum disk size of 528 MB (504 MB under MS-DOS). This means that anything past this mark would not be accessible, unless a different disk addressing scheme (like LBA, Logical Block Addressing) was used.

So for maximum compatibility, the /boot partition is usually located at the start of the disk and ends before cylinder 1024 (528 MB), ensuring that the machine will always be able to load the kernel. The recommended size for this partition on a current machine is 300 MB.

Other reasons for a separate /boot partition are encryption and compression since some methods may not be supported by GRUB 2 yet, or if you need to have the system root partition (/) formatted using an unsupported file system.

# Contents of the Boot Partition

The contents of the /boot partition may vary with system architecture or the boot loader in use, but on a x86-based system you will usually find the files below. Most of these are named with a -VERSION suffix, where -VERSION is the version of the corresponding Linux kernel. So, for example, a configuration file for the Linux kernel version 4.15.0-65-generic would be called config-4.15.0-65-generic.