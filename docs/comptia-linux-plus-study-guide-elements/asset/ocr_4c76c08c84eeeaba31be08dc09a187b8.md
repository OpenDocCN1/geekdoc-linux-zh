your kernel contains drivers for your hard disk controller, so be sure to include the appropriate driver.

+   6.  Exit from the configuration utility.

+   7.  Type **make** to build the new kernel. This process is likely to take several minutes and possibly more than an hour.

+   8.  With 2.4.x or earlier kernels, type **make modules**. This command builds the kernel modules (the parts of the kernel it loads from independent files). This action is handled automatically in step 7 with 2.6.x kernels.

+   9.  As root, type **make modules_install** to install the kernel modules.

+   10. As root, copy the main kernel file to /boot. The file is stored as bzImage in the arch/i386/boot subdirectory of the main kernel directory for x86 systems—change i386 to an appropriate architecture code for other CPUs. I recommend adding the version number to the kernel name, as in `cp arch/i386/boot/bzImage /boot/bzImage-2.6.29`.

+   11. Add the kernel to your boot loader configuration, as described in Chapter 1. Do not replace a working boot loader configuration; add the new kernel to your boot loader. This way, you can fall back on your working configuration if there’s a problem with the new kernel.

+   12. Reboot the computer to use the new kernel.

Most modern distributions rely on an *initial RAM disk* to deliver certain drivers to the kernel. These drivers are needed for reading the hard disk, and an initial RAM disk is a RAM-based pseudo-disk that the boot loader delivers to the kernel, enabling the kernel to read the RAM disk files even if it can’t yet read the actual hard disk. When you recompile a kernel yourself, it’s usually easier to compile the modules into the main kernel file rather than compile them yourself and add them to a RAM disk. If you want or need to build a RAM disk, though, you can do so by using a utility called `mkinitrd`, `mkinitramfs`, or something similar. Details vary from one program or distribution to another, but typically, you’ll use it something like this:

```
# `mkinitramfs -o /boot/initrd-2.6.29.img 2.6.29`
```

This command creates an initial RAM disk called /boot/initrd-2.6.29.img using the modules associated with the 2.6.29 kernel, which must already be compiled and ready on your system. More advanced configuration options are available, but they require intimate knowledge of the Linux boot process.

> You *do not* need to use an initial RAM disk for most kernel drivers, just for drivers that are needed to read files from the hard disk—low-level disk drivers, LVM and RAID drivers, and filesystem drivers. Once the kernel has all the drivers it needs to read your hard disk, it can read additional modules from the hard disk itself.