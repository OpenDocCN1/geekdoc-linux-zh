```
# cat /proc/ide/ide1/hdc/driver
ide-cdrom version 4.53
```

# /proc/scsi/

This is somewhat like /proc/ide, but not as well-organized.

# /proc/pci

This is obsolete. If you run a cat on this, then a dmesg, you'll see a message to that effect. Use the pciutils package, which includes lspci and other programs.

# /proc/ioports

A cat /proc/ioports lists the drivers that use I/O ports on the machine. This is handy for finding conflicts or bad configurations.

# /proc/interrupts

This is like the ioports above, but deals with interrupts. There is one major difference: Devices not currently in use do not show up in this list.

# /proc/devices

This indicates devices configured for files in /dev, along with their major device numbers.

# /proc/partitions

This provides information about current partition tables on all disks.

# /proc/ksyms

This provides the locations of kernel symbols.

# PROBLEM 90

Symptom: You get the error message System is too big. Try using bzImage or modules.
Problem: During compilation, the kernel got too big.
Fix: You probably ran a make zImage or make zdisk instead of a bzImage or bzdisk. Linux has expanded, leaving bzImage (or bzdisk) as the only option for many configurations. After leaving the menuconfig menu, a message appears to the effect that you should run a make zImage (at least, that was true up to kernel version 2.2). Don't listen to that message. Also, use as many modules as possible.