The old IDE model requires only that you have IDE support built in the kernel. Linux will then treat this drive like a normal hard drive, with no additional configuration required. The ATAPI EIDE drive requires that you have support for ATAPI floppy drive in your kernel. To configure either one of these drives, just follow these steps:

+   1. Log in as root.
+   2. Change the directory to the Linux kernel sources directory:
+      `#cd /usr/src/linux`
+   3. Start the kernel's configuration modules by typing the following:
+      `#make menuconfig`
+   4. The kernel configuration module will start; navigate to Block Devices and press Enter.
+   5. Highlight Include IDE/ATA-2 DISK Support and press Y to include it in the kernel.
+      This is for the IDE-based model, not the ATAPI. You'll probably have this already set up if you have an IDE hard drive.
+   6. Highlight Include IDE/ATAPI FLOPPY Support and press Y to include it in the kernel.
+      This is for the ATAPI-based Zip drive.
+   7. Press Esc twice to exit this module.
+   8. Press Esc twice again to exit the kernel configuration module. It will ask you whether you want to save your new kernel configuration; choose Yes.
+   9. Now you need to recompile your kernel for these changes to take effect. To do so, type in the following commands, one after the other:
+      `#make dep`
+      `#make clean`
+      `#make bzImage`
+      `#make modules`
+      `#make modules_install`
+   10. Each of these commands will take some time to execute, and a lot of text will scroll by—don't worry, this is normal. When all the commands have executed, reboot your system.

Reboot your system for the changes to take effect. Pay close attention to the messages the kernel displays as it boots. You should spot your Zip drive being initialized as an IDE device. It will be assigned a device file of the form /dev/hd?.

# SCSI Zip and Jaz Drives

These models are internal (Zip and Jaz) and external (Jaz) and fit in your 3.5- or 5.25-inch drive slots. They are connected to a SCSI controller by a cable. Linux will treat these drives like normal hard drives. You must configure your kernel to support SCSI disks and the SCSI controller to which your drive is connected. To do that, just follow these steps: