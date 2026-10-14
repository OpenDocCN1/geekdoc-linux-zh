With this entry, it is not necessary to specify the partition on each of the following entries.

Note the following regarding the designations for hard disks and partitions:
GRUB does not distinguish between IDE and SCSI hard disks. The hard disk that is recognized by the BIOS as the first hard disk is designated as hd0, the second hard disk as hd1, and so on.
The first partition on the first hard disk is called hd0,0, the second partition hd0,1, and so on.

+   - *kernel /boot/vmlinuz*—This entry describes the kernel location, relative to the partition specified above.
+     It is followed by kernel parameters, such as root=/dev/hda1, vga=normal, etc.
+   - *initrd /boot/initrd*—This entry sets the location of the initial ramdisk (initramfs in SLED 10), relative to the root (hd0,0) specified previously. The initrd contains hardware drivers (such as a driver for the IDE or SCSI controller) that are needed before the kernel can access the hard disk.

The following is an example of the /boot/grub/menu.1st configuration file:

```
```text
# Modified by YaST2. Last modification on Mon May 15 08:38:29 UTC 2006
color white/blue black/light-gray
default 0
timeout 8
gfxmenu (hd0,1)/boot/message

###Don't change this comment - YaST2 identifier: Original name: linux###
title SUSE Linux Enterprise Desktop 10
    root (hd0,1)
    kernel /boot/vmlinuz root=/dev/sda2 vga=0x317 resume=/dev/sda1
splash=silent showopts
    initrd /boot/initrd

###Don't change this comment - YaST2 identifier: Original name: floppy###
title Floppy
    chainloader (fd0)+1

###Don't change this comment - YaST2 identifier: Original name:
failsafe###
title Failsafe -- SUSE Linux Enterprise Desktop 10
    root (hd0,1)
    kernel /boot/vmlinuz root=/dev/sda2 vga=normal showopts ide=nodma
apm=off acpi=off noresume nosmp noapic maxcpus=0 edd=off 3
    initrd /boot/initrd
```
```