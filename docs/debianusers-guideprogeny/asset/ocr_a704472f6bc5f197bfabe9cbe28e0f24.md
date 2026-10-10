# Basic Settings for Linux Entries in the GRUB Boot Manager

| Setting | Comments |
| :--- | :--- |
| title NAME | The name that appears in the GRUB menu. The distribution and version number is usually a good choice. |
| root=PARTITION | The Linux root partition, named using Linux's naming conventions. |
| | Do not confuse with GRUB's root partition or use GRUB's naming convention. |
| kernel PARTITION KERNEL | Use GRUB's naming convention for the partition. |
| | Usually, the kernel is `/boot/vmlinuz`. |