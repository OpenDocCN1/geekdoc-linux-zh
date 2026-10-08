the **bzmage** option. This creates a kernel program called **bzmage** located in the **arch/i386/boot** directory. This kernel file is copied to the **/boot** directory and given the name **vmlinuz-2.6.version**. Then a symbolic link called **/boot/vmlinuz** is created to the kernel **vmlinuz-2.6.version** file. Finally, the modules are created and installed:

```
make dep
make clean
make bzmage
make modules
make modules_install
cp arch/i386/boot/bzmage /boot/vmlinuz-2.6.version
cp System.map /boot/System.map-2.6.version
```

# Kernel Boot Disks

Instead of installing the kernel on your system, you can simply place it on a boot disk or CD-ROM and boot your system from that disc. For a CD-ROM you can first create the kernel as a **bzmage**, install the kernel, and then use **mkbootdisk** to create a bootable CD-ROM. For a boot disk you have the option of creating either a floppy disk directly or a floppy disk image.

If you are using a stripped-down configured version of the kernel that will fit on a 1.44MB floppy disk, you can use the **bzdisk** or **zdisk** options to compile the kernel and install directly on a floppy. You will be need a floppy disk placed in your floppy drive. A standard kernel 2.6 configuration is too large to fit on a floppy, though 2.4 versions will.

For a floppy disk image you can create either a 1.44 or 2.88 image (which will hold the 2.6 kernel). Use the **fdimage** option for a 1.44 image and **fdimage288** for the 1.88 image. Both **fdimage** and **fdimage288** create corresponding floppy disk images in the **arch/i386/boot** directory. They use their own **mtools.conf** configuration located in that directory to generate the letters for the floppy disk image, which **mcopy** can then use to create the images. The **fdimage288** image is often used for virtual users.

```
make bzdisk
make fdimage
make fdimage288
```

> If you are experimenting with your kernel configurations, it may be safer to put a new kernel version on a boot CD-ROM, rather than installing it on your system. If something goes wrong, you can always boot up normally with your original kernel still on your system (though you can always configure your boot loader to access previous versions).

# Boot Loader Configurations: GRUB

If you are using a boot loader such as GRUB or LILO, you can configure your system to enable you to start any of your installed kernels. As seen in the earlier section “Precautionary Steps for Modifying a Kernel of the Same Version,” you can create an added entry in the boot loader configuration file for your old kernel. As you install new kernel versions, you could simply add more entries, enabling you to use any of the previous kernels. Whenever you boot, your boot loader will then present you with a list of kernels to choose from. For example,