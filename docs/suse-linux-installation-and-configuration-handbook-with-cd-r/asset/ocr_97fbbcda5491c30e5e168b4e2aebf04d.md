+   1. Log in as root.
+   2. Change the directory to the Linux kernel sources directory:
+      `#cd /usr/src/linux`
+   3. Start the kernel's configuration modules by typing the following:
+      `#make menuconfig`
+   4. The kernel configuration module will start; navigate to Block Devices and press Enter.
+   5. Highlight Include IDE/ATAPI CDROM Support and press M to make it a module.
+   6. Highlight SCSI Emulation Support and press M to make it a module.
+   7. Press Esc twice to exit this module.
+   8. Navigate to SCSI Support and press Enter.
+   9. Use the arrow keys to highlight the SCSI Support option and press Y to include it in the kernel.
+   10. Highlight SCSI CD-ROM Support and press Y to include it in the kernel.
+   11. Highlight SCSI CD-ROM Generic Support and press Y to include it in the kernel.
+   12. Press the Esc key twice to exit the SCSI support menu.
+   13. Now you need to add support for the CD-ROM filesystem as well. Navigate to Filesystems and press Enter.
+   14. Highlight ISO 9660 CDROM Filesystem Support and press Y to include it in the kernel, or press M to include it as a module that will be loaded only when needed.
+   15. Highlight the Microsoft Joliet CDROM Extensions option and press y to include it. This is a set of extensions that Microsoft added to the CD-ROM ISO 9660 filesystem. A lot of CDs use these extensions, so you should have this.
+   16. Press Esc twice to exit this menu.
+   17. Press Esc twice again to exit the kernel configuration module. It will ask you whether you want to save your new kernel configuration; choose Yes.
+   18. Now you need to recompile your kernel for these changes to take effect. To do so, type in the following commands, one after the other:
+      `#make dep`
+      `#make clean`
+      `#make bzImage`
+      `#make modules`
+      `#make modules_install`
+   19. Each of these commands will take some time to execute, and a lot of text will scroll by—don't worry, this is normal. When all the commands have executed, don't reboot your system yet.

Ok, that takes care of the first step of the configuration. Now, you will have to tell your kernel to make your ATAPI EIDE CD-ROM act like a SCSI CD-ROM. This is done by passing an argument to the kernel when it's booting, which means you must tell LILO (the Linux Loader) to pass it to the kernel when it's booting it. To configure LILO to do that, follow these steps: