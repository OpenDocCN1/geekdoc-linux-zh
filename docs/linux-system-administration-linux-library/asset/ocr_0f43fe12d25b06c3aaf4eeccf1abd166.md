boundary is a point on the disk corresponding to a numbering used by the x86 BIOS to identify sectors on a hard disk. The standard BIOS can't read the 1024th cylinder, and because LILO uses the BIOS, LILO can't read past that, either. LILO 21.3 and later, however, can work around this problem on modern BIOSs (most of those issued since 1998) by using extended BIOS that can read the 1024th cylinder.

If you use a pre-21.3 version of LILO or if your motherboard's BIOS kernel falls below the 1024th cylinder—about 8GB on most systems. If you have a LILO later version than 21.3 and if your BIOS is more recent than 1998, you can place your kernel anywhere. You also need not to be concerned about this if your Linux partitions fall below the 1024-cylinder boundary.

If you need to restrict your kernel's position, one good way to do this is to create a small (5-20MB) partition below the 1024th cylinder and place the kernel in that partition. Typically, this partition is mounted as /boot. Even if you don't create a partition, the Linux kernel often resides in the /boot directory.

To place the kernel file in /boot, you can use a simple cp or mv command:

```
# cp /usr/src/linux/arch/i386/boot/bzImage /boot/bzImage-2.4.0-test8
```

This example copies the bzimage kernel file to a new name. It's a good way to make sure youyou you can easily identify the kernel version, particularly if you experiment with different kernel versions or kernel options.

Installation of the kernel modules is handled by another command in the kernel source directory: make modules_install. This command copies all the compiled kernel modules into a subdirectory of /lib/modules named after the kernel version—for instance, /lib/modules/2.4.0-test8. Once you've placed the kernel and its modules in reasonable locations, you must test Linux to boot the kernel. You can do this by editing /etc/lilo.conf, the LILO configuration file. This file should contain a group of lines resembling the following:

```
image=/boot/mlinux-2.2.16-22
label=linux
itrd=/boot/initrd-2.2.16-22.img
root=/dev/hda7
```