> **NOTE:** Microsoft operating systems require that you use the chainloader to boot them from GRUB.

If you make any changes to the /boot/grub/grub.conf file, you do not need to load those changes. These changes are automatically picked up by GRUB when you reboot your computer. If you are accustomed to using the LILo boot loader, this may confuse you at first, as LILo requires you to rerun the lilo command for the changes to take effect.

# Adding a new GRUB boot image

You may have different boot images for kernels that include different features. These days, as you get updated kernels for Fedora, you simply load an RPM containing the new kernel and that new kernel is added to the grub.conf file as the default kernel to be booted. At boot time, you can choose which kernel you want to run.

> **NOTE:** To avoid having dozens of entries on your boot screen and lots of kernels hanging around, all but the two most recent kernels are removed when you install new kernels on your Fedora system. Likewise, instead of getting lots of boot entries as you add new kernels, only the two most recent kernel entries are maintained in your grub.conf file.

If you build your own kernel, however, or get one to use from another source, you need to modify the grub.conf file yourself to tell Fedora to boot that kernel. Here is the procedure for modifying the grub.conf file:

+   1. Copy the new image from the directory in which it was created (such as /usr/src/kernels/linux-2.6.29-1/arch/i386/boot/) to the /boot directory. Name the file something that reflects its contents, such as bz-2.6.27-1. For example:
+   
+   ```console
+   # cp /usr/src/linux-2.6.31.5-127/arch/i386/boot/bzImage /boot/bz-2.6.31.5-127
+   ```

+   2. Add several lines to the /boot/grub/grub.conf file so that the image can be started at boot time if it is selected. For example:
+   
+   ```console
+   title Fedora (My own IPV6 build)
+   root (hd0,0)
+   kernel /bz-2.6.31.5-127 ro root=/dev/sda2
+   initrd /initrd-2.6.31.5-127.img
+   ```

+   3. Reboot your computer.

+   4. Press Enter at the boot prompt. When the GRUB boot screen appears, move your cursor to the title representing the new kernel and press Enter.

The advantage to this approach, as opposed to copying the new boot image over the old one, is that if the kernel fails to boot, you can always go back and restart the old kernel. When you feel confident that the new kernel is working properly, you can use it to replace the old kernel or perhaps just make the new kernel the default boot definition.