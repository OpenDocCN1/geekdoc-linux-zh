As you can see, it is very small indeed; it takes up a little more than 500KB in uncompressed form. Since it is based on busybox, it has many capabilities. Because busybox is statically linked, it has no dependencies on any system libraries. You will learn more about busybox in Chapter 11.

# 6.5 Using initramfs

initramfs is a relatively new (Linux 2.6) mechanism for executing early user space programs. It is conceptually similar to initrd, as described in the previous section. Its purpose is also similar: to enable loading of drivers that might be required before mounting the real root file system. However, it differs in significant ways from the initrd mechanism.

The technical implementation details differ significantly between initrd and initramfs. For example, initramfs is loaded before the call to do_basic_setup(), which provides a mechanism for loading firmware for devices before its driver has been loaded. For more details, the Linux kernel documentation for this subsystem is relatively up-to-date. See .../Documentation/filesystems/ramfs-rootfs-initramfs.txt.

From a practical perspective, initramfs is much easier to use. initramfs is a cpio archive, whereas initrd is a gzipped file system image. This simple difference contributes to the easy of use of initramfs. It is integrated into the Linux kernel source tree and is built automatically when you build the kernel image. Making changes to it is far easier than building and loading a new initrd image. Listing 6-13 shows the contents of the Linux kernel .../usr directory, where the initramfs image is built. The contents of Listing 6-13 are shown after a kernel has been built.

> 9 do_basic_setup() is called from .../init/main.c and calls do_initcalls(). This causes driver module initialization routines to be called. This was described in detail in Chapter 5 and shown in Listing 5-10.