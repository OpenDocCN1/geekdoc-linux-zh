key to bring up the GRUB2 command line to submit interactive boot commands. Figure 5.1 shows editing an entry in the GRUB2 boot menu on an Ubuntu system.

# **FIGURE 5.1**  Editing an Ubuntu GRUB2 menu entry

![](bbox=[0.25, 0.19, 0.75, 0.43])

Some graphical desktops (such as Ubuntu) hide the GRUB boot menu behind a graphical interface. Usually if you hold down the Shift key when the system first boots, that will display the GRUB boot menu.

# ## Alternative Bootloaders

While GRUB Legacy and GRUB2 are the most popular Linux bootloader programs in use, you may run into a few others, depending on which Linux distributions you use.

The *Syslinux project* includes five separate bootloader programs that have special uses in Linux:

+   * **SYSLINUX:** A bootloader for systems that use the Microsoft FAT filesystem (popular for booting from USB memory sticks)

+   * **EXTLINUX:** A mini-bootloader for booting from an ext2, ext3, ext4, or btrfs filesystem

+   * **ISOLINUX:** A bootloader for booting from a LiveCD or LiveDVD

+   * **PXELINUX:** A bootloader for booting from a network server

+   * **MEMDISK:** A utility to boot older DOS operating systems from the other SYSLINUX bootloaders

The ISOLINUX bootloader is popular for distributions that release a LiveDVD version. The bootloader requires two files: `isolinux.bin`, which contains the bootloader program image, and `isolinux.cfg`, which contains the configuration settings.