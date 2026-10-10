The /proc directory contains many more files than have been presented so far in this chapter. Table 6-2 describes some files that you will find useful when examining a system after installation.

Hardware is detected by the Linux kernel at system startup. However, this information is displayed too quickly to read or hidden by a graphical startup screen. Fortunately, the system logs all information regarding hardware detection and the startup of system processes in log files that can be viewed at a later time.

| Filename | Contents |
| :--- | :--- |
| cmdline | Current location of the Linux kernel |
| cpuinfo | Information regarding the processors in the computer |
| devices | List of the character and block devices that are currently in use by the Linux kernel |
| execdomains | List of execution domains for processes on the system; execution domains allow a process to execute in a specific manner |
| fb | List of framebuffer devices in use on the Linux system; typically, these include video adapter card devices |
| filesystems | List of filesystems supported by the Linux kernel |
| interrupts | List of IRQs in use on the system |
| iomem | List of memory addresses currently used |
| ioports | List of memory address ranges reserved for device use |
| kcore | A representation of the physical memory inside the computer; this file should not be viewed |
| kmsg | Temporary storage location for messages from the kernel |
| loadavg | Statistics on the performance of the processor |
| locks | List of files currently locked by the kernel |
| mdstat | Configuration of multiple-disk RAID hardware |
| meminfo | Information regarding physical and virtual memory on the Linux system |
| misc | List of miscellaneous devices (major number=10) |
| modules | List of currently loaded modules in the Linux kernel |
| mounts | List of currently mounted filesystems |
| partitions | Information regarding partition tables loaded in memory on the system |
| swaps | Information on virtual memory utilization |
| version | Version information for the Linux kernel and libraries |

Table 6-2 Files commonly found in the /proc directory