# 112 Part II ♦ The SUSE System

![](bbox=[0.181, 0.127, 0.818, 0.506])

**Figure 4-2:** The SUSE system boot loader

Selecting the default boot option, Linux, after SUSE has been installed will load the kernel and the initial ramdisk in memory. If you do not specify your Linux menu, the system automatically boots the default choice after ten seconds. The processor will jump to the start of the kernel in memory and execute it. The execution of the kernel is usually very quick, within five seconds. After the kernel has loaded, you will see the initial ramdisk being mounted, and the small Linux distribution takes over and loads any drivers that are needed to load your Linux installation from the disk. SUSE hides much of the boot process behind a graphical screen that simply displays a progress bar. You can press F2 at any time during loading and initialization to see detailed status messages that explain exactly what the system is doing.

The initial ramdisk usually contains essential drivers that are needed to mount your / (root) filesystem. The kernel binary includes the basic drivers for IDE disk devices, those which are not loaded by the initial ramdisk, but the ramdisk, Similarly, the drivers for CD-ROM devices are often loaded from the initial ramdisk. Similarly, the drivers for SCSI devices can either be compiled into the kernel or loaded through the initial ramdisk. The driver for the type of filesystem used on the initial RAM disk must also be compiled into the kernel, but you can load additional filesystem drivers