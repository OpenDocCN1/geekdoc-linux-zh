```
default=0
timeout=10
splashimage=(hd0,4)/grub/splash.xpm.gz
title Red Hat Linux (2.4.22-1)
 root (hd0,4)
 kernel /vmlinuz-2.4.22-1 ro root=LABEL=/ 
 initrd /initrd-2.4.22-1.img
title Windows XP
 rootnoverify (hd0,0)
 chainloader +1
```

The default=0 line indicates that the first partition in this list (in this case Red Hat Linux) will be the one that is booted by default. The line timeout=10 causes GRUB to pause for ten seconds before booting the default partition. (That's how much time you have to press e if you want to edit the boot line, or to press arrow keys to select a different operating system to boot.)

The splashimage line looks in the fifth partition on the first disk (hd0,4) for the boot partition (in this case /dev/hda5, which is the /boot partition). GRUB loads splash.xpm.gz as the image on the splash screen (/boot/grub/splash.xpm.gz). The splash screen appears as the background of the boot screen.

> **NOTE:** GRUB indicates disk partitions using the following notation: (hd0, 0). The first number represents the disk, and the second is the partition on that disk. So, (hd0, 1) is the second partition (1) on the first disk (0).

The two bootable partitions in this example are Red Hat Linux and Windows XP. The title lines for each of those partitions are followed by the name that appears on the boot screen to represent each partition.

For the Red Hat Linux system, the root line indicates the location of the boot partition as the second partition on the first disk. So, to find the bootable kernel (vmlinuz-2.4.22-1) and the initrd initial RAM disk boot image that is loaded (initrd-2.4.22-1.img), GRUB looks in the root of hd0,4 (which is represented by /dev/hda5 and is eventually mounted as /boot). Other options on the kernel line set the partition as read-only initially (ro) and set the root file system to /dev/hda6.

For the Windows XP partition, the rootnoverify line indicates that GRUB should not try to mount the partition. In this case, Windows ME is on the first partition of the first hard disk (hd0,0) or /dev/hda1. Instead of mounting the partition and passing options to the new operating system, the chainloader +1 indicates to hand control the booting of the operating system to another boot loader. The +1 indicates that the first sector of the partition is used as the boot loader.

> **NOTE:** Microsoft operating systems require that you use the chainloader to boot them from GRUB.