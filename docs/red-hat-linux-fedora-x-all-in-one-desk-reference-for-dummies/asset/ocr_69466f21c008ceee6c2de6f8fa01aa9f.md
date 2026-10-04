# Viewing System Information via the /proc File System 417

shown in Table 1-6 are present on your system. The specific contents of the /proc file system depends on the kernel configuration and the driver modules that are loaded (which, in, depend on your PC's hardware configuration.

You can navigate the /proc file system just as you work with any other directories and files in Fedora Core. The more or cat commands used to see the contents of a file.

| Table 1-6 Some Files and Directories in /proc |
| Filename | Content | Book VI Chapter 1 |
|---|---|--|
| /proc/acpi | Information about Advanced Configuration & Power Interface (ACPI) — an industry-standard interface for configuration and power management on laptops, desktops, and servers | |
| /proc/bus | Directory with specific information for each bus type, as PCI | |
| /proc/cmdline | The command line used to start the Linux kernel (for example, ro root=LABEL=/rhdb) | |
| /proc/cpuinfo | Information about the CPU (themicroprocessor) | |
| /proc/devices | Available block and character devices in your system | |
| /proc/dma | Information about DMA (direct memory access) channels that are being used | |
| /proc/driver/rtc | Information about the PC's real-time clock (RTC) | |
| /proc/filesystems | List of supported file systems | |
| /proc/ide | Directory containing information about IDE devices | |
| /proc/interrupts | Information about interrupt request (IRQ) numbers and how they are being used | |
| /proc/iports | Information about input/output (I/O) port addresses and how they are being used | |
| /proc/kcore | Image of the physical memory | |
| /proc/kmsg | Kernel messages | |
| /proc/loadavg | Load average (average number of processes waiting to run in the last 1, 5, and 15 minutes) | |
| /proc/locks | Current kernel locks used to ensure that multiple processes don't write to a file at the same time) | |
| /proc/meminfo | Information about physical memory and swap usage | |
| /proc/misc | Miscellaneous information | |
| /proc/modules | List of loaded driver modules | |