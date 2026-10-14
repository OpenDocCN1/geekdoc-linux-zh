between IDE and SCSI disk drives). The kernel line defines the kernel file that should be booted, with the boot parameters that it uses (ro and root=/dev/hda2 to define the partition for the root file system). The initrd line defines a special file that GRUB loads first to help get the kernel loaded.

+   title DOS: This line assigns a text label to an operating system choice. The two indented lines that follow define a root working partition for GRUB (the MBR in this case). In this case, the rootnoverify indicates that GRUB should not try to understand what is contained on the partition indicated (because it’s not an operating system that GRUB works with directly), but instead assume that a chained boot loader is present on the first sector of that partition, and pass control to it when this operating system is selected.

The grub.conf configuration file is used to define the menu options (and splash screen) presented when you start your computer. You can also install GRUB on the MBR of a computer without using any configuration file by running the grub command as root and using the setup command within GRUB’s interactive shell. Figure 9-4 shows the GRUB shell after executing the help command to list all the commands that GRUB supports.

![](bbox=[0.18, 0.57, 0.68, 0.82])

Figure 9-4 The GRUB shell, listing all GRUB commands

If you install GRUB in this way, then the next time you start your computer, instead of starting an operating system, you will see a GRUB shell prompt. At that point, you can enter a command to start the operating system that you select. Using a configuration file simplifies the use of GRUB.