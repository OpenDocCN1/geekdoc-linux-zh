
The kernel hides the complexities of operating system functions behind simplified program interfaces. For example, when a process wants to open a file, the kernel verifies the access rights, translates the filename into an *inode* number, finds its location on disk, reads it into memory, and then returns a handle to the file to the calling process. The process just makes a simple `open()` system call, and all of the complex activity is transparently handled by the kernel.

The kernel uses device drivers to perform most of its tasks. For example, when opening a file, the kernel translates the file open request into a sequence of I/O requests, such as reading block 12345 from device number 5, and hands that task to the disk device driver to execute.

The kernel provides its services transparently. On behalf of user processes, it performs a host of functions such as reading terminal input, spawning processes, synchronizing process execution, reading and writing files, creating pipes, redirecting I/O, performing network operations, and many other tasks. If the kernel did not do all of these things, then writing a program to do the simplest of jobs would be a Herculean task.

## Why Rebuild the Kernel?

There are several good reasons for reconfiguring and rebuilding the Linux kernel:

- When you install a new Linux system, a generic kernel provided with your distribution is installed. Normally, this generic kernel will operate with your hardware environment, but for efficiency reasons, you should consider recompiling your kernel. Generic kernels are built to support a wide range of devices so that they will work on most of the systems on which you will install Linux. Usually, these kernels include most of the kernel options enabled and a large set of device drivers. This results in a kernel that is versatile, but very large: It consumes more memory than it needs to, takes longer to load, and runs less efficiently. By recompiling your kernel to include only device drivers and options necessary for your system, you can produce a tighter and faster kernel.

- However, this highly efficient smaller kernel comes at the expense of not having support for additional devices that you may need at a future time. Whenever possible, you should build dynamically loadable kernel modules for infrequently used devices. This prevents unnecessary kernel bloating, and when required, the rare device driver module is dynamically loaded. This method provides an optimal solution by keeping the kernel lean while still providing additional hardware device support. However, not all devices can be supported with loadable kernel modules. Refer to the section titled “Understanding Modules” for more details.

- If you add new hardware to your system for which the necessary support has not been compiled for your kernel, you will need to reconfigure and recompile your kernel to integrate the new device driver into your environment.

![](img/6c13bcf02a08ad7923caab46f051d96a_213_0.png)

- As new kernel versions are released, you will need to compile new kernels if you want to upgrade to these newer versions of the Linux kernel. Generally, it is a good idea to keep your kernel up-to-date with the latest stable releases. Newer versions not only offer newer features, but also provide bug fixes, performance improvements, and fixes for security vulnerabilities.

- The kernel runs in a fixed memory space. This limits the maximum number of processes, file handles, and file system buffers to fixed values specified when you compile your kernel. If your system starts hitting these thresholds, erratic behavior will ensue. For instance, new processes may not be able to start, or existing processes may fail when they try to open files. To solve this problem, you may need to recompile your kernel and increase the size of these tables.

## OBTAINING NEW VERSIONS OF THE KERNEL

Kernel source code can be obtained through anonymous FTP from `ftp.kernel.org` in the `/pub/linux/kernel` directory or any of its other mirror sites. To conserve Internet bandwidth, it is advisable to download from a mirror site close to you. The files are distributed as compressed tar archives. The naming convention used is `linux-n.n.n.tar.gz`, where n.n.n is the major.minor.patch number. For example, the current stable release of the kernel at the time of this writing is `linux-2.2.13.tar.gz`. The archives are also available in `.bz2` compression format. The Linux kernel development team follows a version naming convention where, if the minor version is odd, the kernel in question is a development release, while even-numbered minor versions are production releases. For example, version 2.3.x kernels are development releases, and 2.2.x kernels are production releases. Unless you are planning on kernel hacking, it is recommended that you only use production releases.

After downloading the archive, you will need to unpack it. Make sure you have sufficient free space in `/usr/src` before unpacking the archive. `/usr/src` is the standard location for storing kernel source code. At the present time, the source code files are about 14 MB in size, and you will need an additional 70 MB of disk space to successfully compile the kernel.

Source trees for each version of the Linux kernel that you keep on your system will be stored in subdirectories of `/usr/src`. Typically, the source code for the kernel currently in use on your system should be stored in `/usr/src/linux`. Assuming you want to upgrade from version 2.2.5 of the kernel to version 2.2.13 and have downloaded the new source code archive to `/tmp`, use the following steps to install the new kernel’s source code:

```sh
# cd /usr/src
# mv linux linux.2.2.5
# tar zxvf /tmp/linux-2.2.13.tar.gz
# mv linux linux.2.2.13
# ln -s linux.2.2.13 linux
```

## CONFIGURING THE KERNEL

To configure your kernel for compilation, you need to have all the details of the hardware on your system available. You should prepare an inventory of your hardware including, at a minimum, the details of the following devices:

- Disk drives
- Disk controllers
- Floppy drives
- Co-processors
- Network adapters
- Tape drives and controllers
- RAID controllers and arrays
- Graphic adapters
- Mouse
- Terminal interfaces
- Modems
- Printers
- Scanners
- Sound cards
- Other special-purpose devices

With this information in hand, you need to configure the kernel for compilation, a process that will result in a customized makefile.

You can do this with one of three commands:

- **make config**: This command runs a command-line program through which you can choose your kernel options and hardware drivers.
- **make menuconfig**: This command runs a console-based, menu-driven application through which you can choose your kernel options and hardware drivers from a hierarchical structure.
- **make xconfig**: This command runs an X Window System program through which you can choose your kernel options and hardware drivers from a hierarchical structure.

`make menuconfig` and `make xconfig` are easier to use because they display kernel options and drivers in context, which makes it easier to locate, identify, and select them. Using `make xconfig`, you can also view detailed explanations of each option as well as suggested default values for those options. With the X Window option, you can also backtrack as you make choices and only commit to selections after completing your entire configuration. The X Window approach also allows you to complete your configuration over multiple sessions.

Your choices are remembered between invocations of `make xconfig`. When you finally complete your configuration in X Windows and save your changes, the resulting configuration information is stored in a file named `.config`.

With all three configuration methods, each option can be enabled or disabled by selecting y for yes or n for no. Device drivers have a third option: m for module. This option is available for device drivers that are compiled as dynamically loadable modules that can be selectively loaded and unloaded at boot time. These can be loaded after the system has started as needed.

It is important to correctly select several key kernel options:

- **Processor family:** A set of processor family options allows for the selection of your processor type to ensure optimal performance on the target system where the kernel will be used. If you want to build a kernel that will run on any Intel x86-class processor, then you should choose the 386 option.

- **Kernel math emulation:** The math coprocessor is built into the 486 and Pentium-class processors. If you have one of these, then you should not enable this option. If your system CPU type is 386 or 486SX, and the motherboard does not have a 387 or 487 math coprocessor chip, then you need math emulation, and the option should be enabled.

- **Enhanced (MFM/RLL) disk and IDE disk/CD-ROM support:** Unless your disks are all SCSI, you will need to enable this option. If you do so, you have to choose between new IDE drivers and old IDE drivers. The new IDE drivers can support 4 IDE devices (disk and CD-ROM) on a single interface, compared to the old ones that only support two. The new drivers also provide better performance on newer EIDE-type hardware.

- **Networking support:** In almost every instance, you need to enable networking support. Even a home system that connects to the Internet through a dial-up connection requires networking to be enabled. In addition, a standalone system without any form of networking will still require this support to be enabled in the kernel for many applications to work properly.

- **System V IPC:** IPC stands for inter-process communication. Many programs need this feature to communicate with other processes, so this option should be enabled.

- **SCSI support:** If you have any SCSI hardware, you must enable this option. If you do so, you will need to select among several sub-options as outlined in the kernel configuration help files.

- **Network device support:** If the system has a network card, or will participate in dial-up networking, this option should be enabled. If you enable network device support, you will be prompted to select the type of network devices to enable and the protocols for which you need support.

- **File systems:** Linux supports a variety of file systems. The second extended (ext2) file system is mandatory and must be enabled because it is the standard Linux file system.
