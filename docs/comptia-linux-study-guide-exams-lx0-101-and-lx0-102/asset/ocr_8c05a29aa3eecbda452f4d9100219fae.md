# Chapter 5 • Booting Linux and Editing Files

Chainloading as described works on BIOS computers. If you're using an EFI-enabled version of GRUB Legacy, you can chainload, but you must tell GRUB Legacy to use the ESP (typically by specifying root (hd0,0), although the device identification may differ) and then pass the name of an boot loader via the chainloader option, as in chainloader /EFI/Microsoft/boot/bootfw.efi.

To add a kernel to GRUB, follow these steps:

+   1. As root, load the menu. 1st or grub.conf file into the text editor.
2. Copy a working configuration for a Linux kernel.
3. Modify the title line to give your new configuration a unique name.
4. Modify the kernel line to point to the new kernel. If you need to change any kernel options, do so.
5. If you're adding, deleting, or changing a RAM disk, make appropriate changes to the initrd line.
6. If desired, change the default line to point to the new kernel.
7. Save your changes, and edit the text editor.

At this point, GRUB is configured to boot your new kernel. When you reboot, it should appear in your menu, and you should be able to boot it. If you have problems, boot a working configuration to debug the issue.

![](bbox=[0.133, 0.555, 0.233, 0.603])

# Installing GRUB Legacy

The command for installing GRUB Legacy on a BIOS-based computer is grub-install. You must specify the boot sector by device name when you install the boot loader. The basic command looks like

```
# grub-install /dev/sda
```

or

```
# grub-install `(hd0)`
```

Each command will install GRUB Legacy into the first sector (that is, the MBR) of your first hard drive. In the second example, you need single quotes around the device name. If you want to install GRUB Legacy in the boot sector of a partition rather than in the MBR, you include a partition identifier, as in /dev/sda1 or (hd0,0).