+   kernel—Defines the kernel image file stored in the `/boot` folder to load.
+   `initrd`—Defines the initial RAM disk file, which contains drivers necessary for the kernel to interact with the system hardware.
+   `rootnoverify`—Defines non-Linux boot partitions, such as Windows.

The `root` command defines the hard drive and partition that contains the `/boot` folder for GRUB Legacy. Unfortunately, GRUB Legacy uses a somewhat odd way of referencing those values:

        (hd`, `partition`)

Also, unfortunately, GRUB Legacy doesn’t refer to hard drives the way Linux does; it uses a number system to reference both disks and partitions, starting at 0 instead of 1. For example, to reference the first partition on the first hard drive on the system, you’d use `(hd0,0)`. To reference the second partition on the first hard drive, you’d use `(hd0,1)`. The `initrd` command is another important feature in GRUB Legacy. It helps solve a problem that arises when using specialized hardware or filesystems as the root drive. The `initrd` command defines a file that’s mounted by the kernel at boot time as a RAM disk, also called the `initrd`. The kernel can then load modules from the `initrd` RAM disk, which then allows it to access hardware or filesystems not compiled into the kernel itself. The `initrd` RAM disk file, located in the `/boot` directory, is called `initrd.img-kversion`, where `kversion` is the kernel version number.

![](bbox=[0.11, 0.51, 0.17, 0.58])

If you install new hardware on your system that’s required to be visible at boot time, you’ll need to modify the `initrd` file. You can create a new `initrd` RAM disk image containing modules for the new hardware using the `mkinitrd` command in Red Hat–based systems. For Debian–based systems, the file is called `initramfs`, and you create it using the `mkinitramfs` command. Alternatively, you can use the `dracut` utility, which creates the `initramfs` image from a framework and copies files from the installed modules.

Listing 5.2 shows a sample GRUB configuration file that defines both a Windows and a Linux partition for booting.

# **Listing 5.2**
Sample GRUB Legacy configuration file

```
default 0
timeout 10
color white/blue yellow/blue

title Ubuntu Linux
root (hd1,0)
kernel (hd1,0)/boot/vmlinuz
```