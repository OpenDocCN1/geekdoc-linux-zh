# Global section

The first part of /etc/lilo.conf begins with the instruction boot= specifies where LILO is to be installed. For installation on a diskette, the specification is /dev/fd0. To install LILO into the MBR of the first IDE hard disk, use /dev/hda for the first SCSI disk, /dev/sda.

delay specifies how tens of seconds LILO waits for input. The shortest delay is 0, but you must keep Shift depressed before you start LILO if you do not want to use the default operating system.

prompt has the opposite effect and forces a user input before the boot process is started. In this case, arrow causes the default operating system to be booted. All operating systems can be selected as described above, prompt prevents unintended reboot.

compact allows a particularly fast loading of the kernel (all above, from the diskette), but it does not work on all computers or with hard disk controllers.
The map allows you to specify the file in which the sector numbers of the kernel files and other files are stored. /boot/map is used, which is usually a sensible default setting.

A further option which is often omitted is install specifies the file in which the LILO main program (the second stage loader) is. The default setting is /boot/map and needs to be changed only in rare cases.
The linear option causes the sector addresses in /boot/map not to be stored as CHS tuples (cylinder, head, sector), but as LBA values (Logical Block Addressing). See page 33. When LILO and the BIOS agree on a common interpretation of the hard disk geometry, using linear is the easiest solution.

According to the SuSE database, the linear option reduces the maximum address range depending on the CHS geometry signaled by the BIOS. The reason for this is 16-bit arithmetic used in the calculation of sector numbers. Under unfavorable circumstances - in particular with a CHS geometry of more than 64 sectors per track - as commonly used by current LILO versions - linear allows only a smaller area of the disk to be addressed and it would be possible without this option (which, depending on the BIOS, up to 7.9 Gigabytes).

```
# /etc/lilo.conf (part 1)
# LILO global section
boot=/dev/fd0          # installation in the MBR of a diskette
delay=100             # wait 10 seconds
#prompt                # force input (no automatic start)
#compact               # faster, especially with disks; can cause problems with some hard disks
map=/boot/map          # default setting in any case
install=/boot/boot.b   # default setting in any case
#linear                 # required for some hard disks
```

In some cases (big disks, old BIOS, and so on), LILO has problems with the hard disk geometry. As a first solution, you should try the linear option.