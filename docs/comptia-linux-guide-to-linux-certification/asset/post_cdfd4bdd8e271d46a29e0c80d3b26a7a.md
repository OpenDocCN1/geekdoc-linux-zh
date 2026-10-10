
at boot time, you simply need to add the line `zfs mount datastorage1 datastorage2 datastorage3 datastorage4` to a system startup script. System startup scripts are discussed in Chapter 8.

## Installing a Linux Server Distribution

Any Linux distribution can be used as a server if the necessary packages are installed that provide for server services on the network. However, many Linux distributions also provide a version that is geared for Linux servers. These **Linux server distributions** do not have a GUI environment installed by default, since administration of Linux installed on a rackmount server is often performed using commands within a BASH terminal on a remote computer across the network. Instead, most Linux server distributions ship with a set of packages that are commonly used on Linux servers, including Web server, database server, file server and email server software.

![](img/c27875544958897d817484d558c208c8_300_0.png)

Remote administration methods are discussed in Chapter 12.

![](img/c27875544958897d817484d558c208c8_300_1.png)

The configuration of common server software packages is covered in Chapter 13.

The installation process for a Linux server distribution differs from a standard or live Linux installation process. No GUI environment is loaded during the installation process, and the installation program often prompts you for additional information that is necessary for a server, such that you don’t need to configure that same information afterwards, including:

- *The host name and IP configuration of the server*—For a desktop system, the default hostname (localhost) will often suffice. However, for a server system, the host name is often used by the configuration of server services and should match the name that other computers on the network will use when contacting the server. Additionally, many Linux administrators prefer to configure a static IP address on server systems rather than obtain an IP address automatically. This ensures that the IP address of the server cannot change over time.

- *Whether to allow for automatic updating*—Most Linux systems are configured by default to download important OS and application updates periodically. However, for a Linux server, an update could potentially cause problems with software that is currently running on the server. As a result, most Linux administrators prefer to manually update software after testing the update on a non-production computer that contains the same software as the server. Application updates will be discussed in more depth in Chapter 11.

- *Package selection*—While most Linux distributions automatically install a predefined set of software packages during installation without user input, Linux server distributions often prompt you to select the specific software packages that will be needed on the Linux server. This prevents unnecessary packages from being installed and space from being wasted on the server filesystems.

- **Server service configuration**—Some server service packages that are installed require additional configuration in order to provide functionality. The installation program for a Linux server distribution may prompt you for that information during the installation so that you don’t need to configure it afterwards.

- **Boot loader configuration**—During the Fedora installation program, you are not prompted to supply information regarding the boot loader that will be used to boot the Linux kernel. However, most Linux server distributions prompt you for the location of the Linux boot loader during the installation. GRUB (GRand Unified Boot loader) is the standard boot loader used on Linux systems. By default, most Linux distributions install the first part of GRUB on the MBR/GPT (e.g., /dev/sda). However, you can also choose to install the first part of GRUB on the first sector of the Linux partition that holds the kernel (e.g., /dev/sda1) if you have one or more operating systems already installed on the server system in a multi-boot configuration. Boot loaders will be discussed in more depth in Chapter 8.

![](img/c27875544958897d817484d558c208c8_301_0.png)

In Hands-on Project 6-1, you will install the Ubuntu Server 14.04 Linux distribution. In addition to providing the opportunity to install a Linux server distribution, this project will allow you to apply concepts in later chapters to more than one Linux distribution, as well as configure Linux components that are not found in Fedora Linux, such as the Debian Package Manager, the SysV initialization system, and the system log daemon.

Since servers provide a critical role within the organization, it is important to verify that the installation process has completed successfully and that all hardware components are working properly with the OS after installation.

## Dealing with Problems During Installation

Most problems that occur during a Linux installation are related to faulty hardware or an incorrect device driver for a hardware component. In both of these cases, the installation may end abnormally and a “fatal signal 11” error message may appear on the screen. This indicates an error, known as a segmentation fault, in which a program accesses a certain area of RAM that was not assigned. If a segmentation fault occurs when you are installing Linux, first check the RAM for errors by running the memtest86 utility shown in Figure 2-6. The memtest86 utility is included on nearly all Linux installation media and can be run from the welcome screen that first appears when you boot the computer from the installation media.

If you experience a segmentation fault during installation and the memtest86 utility finds no RAM errors, first check with the hardware manufacturer of the system (as well as the hardware manufacturer of any additional hardware devices added to the system prior to installation) to determine if an updated driver is available for your distribution of Linux. If one is available that is needed during the installation process (e.g., for a new disk controller card), the manufacturer will often provide instructions that allow you to specify the new driver during the installation process. If you are installing from live media, this is often performed by activating the driver after the live Linux system has loaded. Alternatively, if you are installing from standard installation media, the location of the driver is often specified by modifying the default installation boot options at the welcome screen when you boot the Linux installation media. To access the default installation boot options for Fedora 20, you can press the Tab key at the welcome screen shown in Figure 2-4.

If you experience a segmentation fault during installation and both your RAM and device drivers appear functional, you can assume that some hardware component is faulty. Zeroing in on the right piece of hardware can be tricky. Often, you can fix segmentation faults by turning off the CPU cache memory or by increasing the number of memory wait states in the BIOS. On some computers, the BIOS allows the user to change the voltage for the RAM and CPU; incorrect values could be the source of a segmentation fault. Other causes include power management conflicts and overclocked CPUs.

![](img/c27875544958897d817484d558c208c8_302_0.png)

> An **overclocked** CPU is a CPU that is faster than the speed for which the processor was designed. Although this might lead to increased performance, it also makes the processor hotter and can result in intermittent computer crashes.

![](img/c27875544958897d817484d558c208c8_302_1.png)

If the installation fails with an error other than fatal signal 11, consult the support documentation for your distribution of Linux, or check Internet newsgroups and forums.

In some cases, the installation process fails to place a boot loader on the hard disk properly; this often occurs with older generation hard disk drives that have over 1024 cylinders. To avoid this problem, ensure that the `/` partition starts before the 1024th cylinder (the 8GB mark on most hard disks) or create a partition for the `/boot` directory that starts before the 1024th cylinder.

## Dealing with Problems After Installation

Even after a successful Linux installation, problems might arise if the installation program failed to detect the computer's hardware properly or if certain programs were not installed as expected. To ensure no such problems occurred, check the **installation log files** after installation and then verify system settings to ensure that all hardware was detected with the correct values.

The **installation log files** are files that are created by the installation program that record the events that occurred during the installation process, including errors. For Fedora Linux, these log files are stored in the `/var/log/anaconda` directory; and for Ubuntu Server Linux, these log files are stored in the `/var/log/installer` directory. To search these files for errors and warnings, you should use the `grep` command, as their contents are often quite lengthy. For example, the `grep -i "(error|warn)" /var/log/anaconda/*` command can be used to search for any errors or warnings within the log files in the `/var/log/anaconda` directory.

To verify hardware settings, you can examine the content of the `/proc` directory or boot-up log files. The `/proc` directory is mounted to a special filesystem contained within RAM that lists system information made available by the Linux kernel; because this is an administrative filesystem, all files within are readable only by the root user. The following sample listing of the `/proc` directory shows many file and subdirectory contents:

```
[root@server1 ~]# ls -R /proc
1/   1171/  171/  3/   415/  48/  801/    kallsyms  softirqs
10/  12/    172/  300/ 417/  484/ 9/    kcore     stat
```
