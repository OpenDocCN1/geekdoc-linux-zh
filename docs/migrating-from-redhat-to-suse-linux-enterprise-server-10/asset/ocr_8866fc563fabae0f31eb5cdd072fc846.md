+   * **Other.** When you select this, a drop-down menu with the following additional choices opens up:

+       * **Edit Configuration Files.** Display and edit the configuration files (/boot/grub/device.map, /boot/grub/menu.lst, or /etc/grub.conf).
+   
+           Note: /etc/grub.conf on SLES 10 contains the information needed to install the bootloader (`grub --batch < /etc/grub.conf`), while the same file on RHEL has the same content as /boot/grub/menu.lst.

+       * **Propose New Configuration.** This option generates a new configuration suggestion. Older Linux versions or other operating systems found on other partitions are included in the boot menu, enabling you to boot Linux or its old boot loader. The latter takes you to a second boot menu.

+       * **Start from Scratch.** This option lets you create the entire configuration from scratch. No suggestions are generated.

+       * **Reread Configuration from Disk.** If you already performed some changes and are not satisfied with the result, you can reload your current configuration with this option.

+       * **Propose and Merge with Existing GRUB Menus.** If another operating system and an older Linux version are installed in other partitions, the menu is generated from an entry for the new SUSE Linux, an entry for the other system, and all entries of the old boot loader menu. This procedure might take some time and is only available with GRUB.

+       * **Restore MBR from Hard Disk.** The MBR saved on the hard disk is restored.

+   1. When you finish configuring the boot loader, save the configuration changes by selecting **Finish**.