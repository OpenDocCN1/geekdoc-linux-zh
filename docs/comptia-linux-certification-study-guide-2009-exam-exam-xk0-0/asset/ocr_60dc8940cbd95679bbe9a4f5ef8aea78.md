+   9. Type `chroot /mnt`.

+   10. Type `passwd root` [to reset the root password].

+   11. Enter new root password: ` < >`

+   12. Type `exit` [to leave the chroot environment].

+   13. Type `umount /mnt` [to unmount the filesystem].

+   14. Reboot the system.

# SUMMARY OF EXAM OBJECTIVES

In this chapter, we discussed the Linux boot process and the information you will be required to know during the booting of a Linux system. The Linux boot process was presented in four stages. The four stages were the powering-up of your system, loading and executing GRUB, loading and executing the Linux kernel, and loading the root filesystem. After presenting an overview of the Linux boot process, details were presented for three key components of the Linux boot process.

For the first section, GRUB, the default bootloading application was introduced. GRUB's purpose is to perform a sequence of events on your computer to load the main operating system. In essence, the bootloader receives control from the system BIOS process, performs a sequence of events, and then transfers control to the operating system kernel. The GRUB program was presented in two forms. The preinstallation form normally used during the initial booting of your system, and the postinstallation form normally used as an application to install or test GRUB configuration settings before applying the modifications to the system during the boot process.

For the preinstallation form, GRUB stages 1 and 2 were introduced to describe how the Linux kernel and mass storage devices are accessed. For the postinstallation form, three critical GRUB configuration files were presented. The /etc/grub.conf, /boot/grub/menu.lst, and /boot/grub/device.map are the three files. Each of the three configuration files are used during the Linux boot process, however, it is during postinstallation that the files are typically modified and tested by the GRUB shell command.

In addition, during the postinstallation two GRUB commands are presented. The two commands are grub-batch and grub-install. The grub-batch command is used to implement changes made to the GRUB configuration device.map file and reloads the device.map file before executing commands listed in the grub.conf file. The grub-install command is used to reinstall the GRUB preinstallation application to the hard disk