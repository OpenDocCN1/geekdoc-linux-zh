# Installing the Source Files and Rebuilding the Kernel

Rebuilding the kernel refers to the task of creating a new binary file for the core Linux operating system. This binary file runs when Red Hat Linux boots. You may have to build the kernel for various reasons:

+   - After you apply kernel patches that update the operating system’s source files, you have to rebuild the kernel and reboot the system to use the new kernel.
+   - After you initially install Red Hat Linux, you may want to create a new kernel that includes support for only the hardware actually installed on your system. In particular, if you have a SCSI adapter, you may want to create a kernel that links in the SCSI driver. The kernel in the companion CD-ROMs includes the SCSI driver as an external module that you must load at startup.
+   - If you have a system with hardware for which only experimental support is available, you have to rebuild the kernel to include that support in the operating system.

![](bbox=[0.16, 0.5, 0.27, 0.58])

Before you rebuild the kernel, make sure you have the emergency boot floppy (covered in Session 3) that you prepared when installing Red Hat Linux. If the system does not boot after you rebuild the kernel, you can use that emergency boot floppy to start the system and repeat the kernel build process.

![](bbox=[0.16, 0.6, 0.27, 0.68])

Never rebuild and install a new kernel without first making sure that you have an emergency boot floppy. If you did not create the boot floppy during Red Hat Linux installation, use the /sbin/mkbootdisk command to create the boot floppy. Type man mkbootdisk to learn the syntax of that command.

Rebuilding the kernel involves the following key phases:

+   - Installing kernel source files
+   - Configuring the kernel
+   - Building the kernel
+   - Building and installing the modules (if any)
+   - Installing the kernel and setting up LILO

Subsequent sections describe the phases of kernel building.