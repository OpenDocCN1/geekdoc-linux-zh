+   **fs.** This directory contains the implementation of filesystems such as EXT3, EXT4, reiserfs, FAT, VFAT, sysfs, procfs, isofs, JFFS2, XFS, NTFS, and NFS.

+   **include.** Kernel header files live here. Subdirectories prefixed with asm contain headers specific to the particular architecture. So the directory include/asm-x86/ contains header files pertaining to the x86 architecture, whereas include/asm-arm/ holds headers for the ARM architecture.

+   **init.** This directory contains high-level initialization and startup code.

+   **ipc.** This contains support for Inter-Process Communication (IPC) mechanisms such as message queues, semaphores, and shared memory.

+   **kernel.** The architecture-independent portions of the base kernel can be found here.

+   **lib.** Library routines such as generic kernel object (kobject) handlers and Cyclic Redundancy Code (CRC) computation functions stay here.

+   **mm.** The memory management implementation lives here.

+   **net.** Networking protocols reside under this directory. Protocols implemented include Internet Protocol version 4 (IPv4), IPv6, Internetwork Protocol eXchange (IPX), Bluetooth, ATM, Infrared, Link Access Procedure Balanced (LAPB), and Logical Link Control (LLC).

+   **scripts.** Scripts used during kernel build reside here.

+   **security.** This directory contains the framework for security.

+   **sound.** The Linux audio subsystem is based in this directory.

+   **usr.** This currently contains the initramfs implementation.

![](bbox=[0.06, 0.69, 0.83, 0.79])

Wading through these large directories in search of symbols and other code elements can be a tough task. The tools in Table 1.1 are worthy aids as you navigate the kernel source tree.