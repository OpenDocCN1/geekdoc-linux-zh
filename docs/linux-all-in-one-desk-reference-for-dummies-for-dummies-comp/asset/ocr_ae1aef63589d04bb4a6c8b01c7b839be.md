Here’s what some of the lines in the GRUB menu file mean (the lines that begin with # are comments):

+   • `default 0:` Specifies the first boot entry as the default one that GRUB boots. If this line is set to 1, GRUB boots the second entry (2 means the third entry, 3 is the fourth, and so on).

+   • `timeout 5:` Causes GRUB to boot the default entry automatically after waiting for 5 seconds. If other boot entries are in the file, the user may select another one from a boot menu that GRUB displays.

+   • The lines starting with `title` constitute the first boot entry or section (the next entry begins with another `title` line), and this entry defines a specific kernel file GRUB can boot. You can make GRUB boot another kernel by adding a similar section to the configuration file. Here’s the meaning of the lines in this boot entry:

+   • `root (hd0,4):` Sets the root device to the first logical partition of the first hard drive. This partition is where the Linux kernel for Ubuntu is installed on this particular system.

+   • `kernel /vmlinuz-2.6.10-5-386 root=/dev/hda9 ro acpi=off quiet splash:` Identifies the kernel that GRUB loads if the user selects this boot entry. In this case, the kernel file is `/vmlinuz-2.6.10-5-386`, which is located in the root device. In a Linux system, that partition is typically mounted on the `/boot` directory. In other words, GRUB loads the kernel file `/boot/vmlinuz-2.6.10-5-386.` The items following the kernel name are options provided to the kernel. For example, the `root` option identifies the partition containing the `root` filesystem `(/)` .

+   • `initrd /initrd.img-2.6.10-5-386:` Specifies a file that contains an initial RAM disk (`initrd`) image that serves as a file system before the disks are available. The Linux kernel uses the `RAM disk` — a block of memory used as a disk — to get started; then it loads other driver modules and begins using the hard drive.

+   • The next section that begins with `title` is for booting Xandros from the third partition of the second IDE drive. Xandros uses the LILO bootloader, and this boot entry uses GRUB’s `chainloader` command to transfer control to the LILO bootloader.

+   • The next section starting with `title Windows XP` is the third boot entry and refers to the Windows XP operating system that happens to be on this system. The text next to the title line appears in the GRUB menu from which the user selects which operating system to boot.