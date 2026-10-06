root=/dev/hda3 — Sets the root device

vga=791 — Sets the framebuffer resolution to 1024 × 768

See Chapter 8 for more information on framebuffer graphics and resolution.

+   - acpi-off — Disables Advanced Configuration and Power Interface (ACPI),
  required on troublesome hardware

+   - ide=nome — Disables Direct Memory Access (DMA) access to IDE disks

+   - noaptic — Does not use the APIC interrupt controller

These three lines will be seen as part of the failsafe entry in /boot/grub/
menu.lst because each of them can solve common problems with particular
hardware.

# The Initial Ramdisk

As the system boots, it needs drivers for the disk controllers and the filesystems
hard disk; otherwise, it will not be able to mount the disks. The necessary
drivers may not be included in the kernel itself but loaded as drivers. This is not a
blem on the running system can create a "chicken and egg" situation at boot
time. The problem is solved by loading the initrd memory at boot time.
(Typically the initrd is whatever is pointed to by the symbolic link
/boot/initrd, but a different initrd can be specified if required in the GRUB menu
/boot/grub/menu.lst) The initrd is fact a compressed EXT2 filesystem that is
decomressed and loaded into memory at initial boot time. The initrd and the ker-
nel are loaded in the system from known physical locations on the
device (in case of LILO) or through the use of a boot loader that is capable
of reading the filesystem from the outside (in the case of GRUB). The initrd is
temporarily by the kernel prior to the mounting of the disk partitions.
Exactly what the initrd includes is in the file /etc/sysconfig/kernel in the
TR_MODULES variable. On a desktop machine, this may simply look like:

```
INITRD_MODULES="reisfers",
```

If have SCSI, it will almost certainly need to include a driver for the disk
controller. This will be normally handled correctly during installation, but there
occasions when you may need to change this manually. Having done, you will
need to run the command mkinitrd to create a new initrd with the correct modules
included. After the initrd has been created, if you reboot, the necessary support
sbe present.