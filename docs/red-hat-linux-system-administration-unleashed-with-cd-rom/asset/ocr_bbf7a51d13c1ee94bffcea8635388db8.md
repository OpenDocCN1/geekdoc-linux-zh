# When Not to Use Modules

There are parts of your kernel that should usually not be built as modules. These parts include the filesystem driver used by your root partition, normal hard drive support, network support, and TCP/IP support. In addition, if you do not want to rely on the initial RAM disk feature of the kernel, you should not compile the driver for your boot disk SCSI controller (if you boot from a SCSI drive). All of these items are required to boot the kernel.

You can opt to build some of these items as modules provided that you include support for an initial RAM disk in your kernel. The initial RAM disk is loaded by the boot loader and loads modules required to continue booting the system. The Red Hat distributed kernel includes this support and uses the initial RAM disk to load SCSI drivers required to boot the system. The initial RAM disk alters the manner in which the kernel is booted, causing system startup to occur in two phases. The initial phase brings up the kernel with a minimal set of compiled in drivers, loads the initial RAM disk as the root filesystem, and then executes commands to load additional modules required to complete the boot process.

# Booting the System Utilizing Initial RAM Disk Support

These are the steps in booting the system when utilizing the initial RAM disk support:

+   1. The boot loader loads the kernel and creates the initial RAM disk.
+   2. The initial RAM disk is converted to a normal RAM disk and the memory used by the initial RAM disk is freed.
+   3. This new RAM disk is mounted read/write as the root filesystem.
+   4. An executable (program or script) called /linuxrc is executed. This script normally is used to load modules required to complete booting the system.
+   5. Upon termination of the /linuxrc script or program, the root filesystem is mounted. The root filesystem in this case is the one built in to the kernel.
+   6. If a directory called /initrd exists on the root filesystem, the initial RAM disk is moved to it, otherwise it is unmounted.
+   7. The normal boot sequence then commences with the invocation of the init process, using the new root filesystem.

With this basic knowledge of what modules are, when to use them, and why they are useful, we are ready now to proceed with configuring the Linux kernel.