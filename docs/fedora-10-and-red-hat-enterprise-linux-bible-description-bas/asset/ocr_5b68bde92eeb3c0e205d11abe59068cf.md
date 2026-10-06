# ## Chapter 2: Installing Fedora

kernel and that new kernel is added to the grub.conf file as the default kernel to be booted.
At boot time, you can choose which kernel you want to run.

> NOTE: To prevent you from having dozens of entries on your boot screen and lots of kernels hanging around, when you install new kernels on your Fedora system, all but the two most recent kernels are removed. Likewise, instead of getting boot entries as you add new kernels, only the two most recent kernel entries are maintained in your grub.conf file.

If you build your kernel, however, or get one from another source, you need to modify the grub.conf file yourself to tell Fedora or RHEL to boot your kernel. Here is the procedure for modifying the grub.conf:

+   1. Copy the new image from the directory in which it was created (such as /usr/src/kernels/linux-2.6.27-1/arch/i386/boot) to the /boot directory. Name the file that reflects its contents, as bz-2.6.27-1. For example:
   `cp /usr/src/linux-2.6.27-1/arch/i386/boot/bzImage /boot/bz-2.6.27-1`

+   2. Add several lines to the /boot/grub/grub.conf file so that the image can be started at boot time if it is. For example:
   title Fedora (My own IPv6 build)
   root (hd0,1)
   kernel /bz-2.6.27-1 root=/dev/sda2
   initrd /inittrrd-2.6.20-5.img`

+   3. Reboot your computer.

+   4. Press Enter. When the GRUB boot screen appears, move your cursor to the title representing the new kernel and press Enter.

The advantage of this, as opposed to copying the new boot image over the old one, is that if the kernel fails to boot, you can always go back and restart the old kernel. When you feel confident that the new kernel is working properly, you can use it to replace the old kernel or perhaps just make the new kernel the default boot definition.

# # Troubleshooting Installation

The description of troubleshooting Fedora or RHEL installation is split into three different areas. The first is what to try if you fail to install Fedora or RHEL. Next’s what to do if it installs, but fails to boot up. The final area describes how to go forward if Fedora or RHEL is basically working, but certain features or hardware components are not working.

Insert your Fedora or RHEL boot media and reboot your computer. If your computer bypasses the DVD or CD completely and boots right from hard disk, you may need to change the BIOS (as described earlier in this chapter). If the DVD or CD drive keeps blinking, but doesn’t