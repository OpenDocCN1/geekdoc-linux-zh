
## Types of Boot Configurations

The type of boot configuration chosen for a system greatly influences the selection of a bootloader, its configuration, and the type of software and hardware found in the host. A network boot configuration, for example, requires that the host provide some types of network services to the target. In designing your system, you first need to identify the boot configurations you are likely to use during development and in the final product. Then, you need to choose a bootloader or a set of bootloaders that will cater to the different types of boot setups you are likely to use. Not all bootloaders, for example, can boot kernels from disk devices. In the following discussion, we will cover the possible boot configurations. Let us start, nevertheless, by reviewing some boot basics.

All CPUs fetch their first instruction from an address preassigned by their manufacturer (occasionally with some design flexibility between a few alternative addresses—determined by strapping lines on the CPU). Any system built using a CPU has one form or another of a solid-state storage device at that location. Traditionally, the storage device was a masked ROM, but flash chips are increasingly the norm today. The software on this storage device is responsible for bootstrapping the system. The level of sophistication of the boot software and the extent to which it is subsequently used as part of the system’s operation greatly depend on the type of system involved.

Masked ROMs continue to be used when devices are produced in very large quantities. Consumer gaming devices such as consoles, for example, often use masked ROMs.

Some higher-end FPGA platforms running Linux don’t even use regular memory at all. They create special block RAM devices with “hard-wired” jump instructions at the regular CPU reset vector, designed to force it to jump to bootloader code preloaded into RAM by the same special hardware device that also loaded the FPGA configuration itself.

Such an approach is extremely popular in designs based around the Xilinx Virtex family of FPGAs. In this case, a mere five hardcoded PowerPC instructions are all that are required to be “hard-wired” into synthetic block RAM at the reset vector, sufficient to jump into a preloaded bootloader.

On most workstations and servers, the boot software is responsible only for loading the operating system from disk and for providing basic hardware configuration options to the operator. In contrast, there are very few agreed upon purposes, if any, for boot software in embedded systems, because of the diversity in purposes of embedded applications. Sometimes, the boot software will run throughout the system’s lifetime. The boot software may also be a simple monitor that loads the rest of the system software. Such monitors can then provide enhanced debugging and upgrading facilities.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_70_0.png)

Figure 2-5. Typical solid-state storage device layout

The boot software may even load additional bootloaders, as is often the case with x86 PCs.

Embedded Linux systems are as diverse as their non-Linux counterparts. They are characterized, nevertheless, by the requirement to load a Linux kernel and its designated root filesystem. How these are loaded and operated largely depends on the system's requirements and sometimes on the state of its development, as described earlier in “Types of Host/Target Development Setups.”

There are three different setups used to bootstrap an embedded Linux system: the solid-state storage media setup, the disk setup, and the network setup. Each setup has its own typical configurations and uses. The following subsections will discuss each setup in detail.

In Chapter 9, we will discuss the setup and configuration of specific bootloaders for each applicable setup.

### Solid-State Storage Media

In this setup, a solid-state storage device holds the initial bootloader, its configuration parameters, the kernel, and the *root* filesystem. Although the development of an embedded Linux system may use other boot setups, depending on the development stage, most production systems contain a solid-state storage media to hold all the system's components. Figure 2-5 shows the most common layout of a solid-state storage device with all the system components.

No memory addresses are shown in Figure 2-5, because the ranges vary greatly. Intuitively, you may think that addresses are lower on the left and grow toward the right. However, there are cases where it is the inverse, and the bootloader is at the top of the storage device address range instead of the bottom. For this reason, many flash devices are provided in both top- and bottom-boot configurations. Depending on the configuration, the flash region where the bootloader is found often has special protection mechanisms to avoid damage to the bootloader if a memory write goes astray. In top-boot flash devices, this protected region is located at the top of the device's address range, whereas in bottom-boot flash devices, it is located at the bottom of the device's address range.

Although Figure 2-5 shows the storage device separated into four different parts, it may contain fewer parts. The boot parameters may be contained within the space reserved for the bootloader. The kernel may also be on the root filesystem (as is the case in popular devices, such as the OLPC “$100 laptop,” which uses an OpenFirmware filesystem-aware bootloader). This, however, requires that the bootloader be able to read the root filesystem. Also, the kernel and the root filesystem could be packaged as a single image that is uncompressed in RAM before being used (in fact, 2.6 Linux kernels make this process particularly easy, if desired).

Depending on the capabilities provided by your bootloader, there may even be other possible configurations, each with its advantages and disadvantages. Usually, a setup can be categorized along a set of four criteria: flash memory use, RAM use, ease of upgrading, and bootup time.

Boot storage media are initially programmed using a device programmer—for example, in mass-produced devices on a large yield production line—or the CPU’s integrated debug capabilities, such as JTAG or BDM. Once the device is initially programmed, it can be reprogrammed by the system designer using the bootloader, if it provides this capability, or using Linux’s MTD subsystem (MTD stands for “memory technology device”). The system may also contain software that enables the user to easily update the storage device. We will discuss the programming of solid-state storage media in Chapter 7.

### Disk

This is the setup you are probably most familiar with because of its widespread use in workstations and servers. Here, the kernel and the root filesystem are located on a disk device. The initial bootloader (which is normally resource constrained; for example, PC-based systems require that it fit into a 512-byte “boot sector”) either loads a larger and more powerful secondary bootloader from the disk or fetches the kernel itself directly from the disk. One of the filesystems on the disk is then used as the root filesystem.

During development, this setup is particularly attractive if you would like to have a large number of kernel and root filesystem configurations for testing. If you plan to develop your embedded system using a customized mainstream distribution, for instance, this setup is convenient. If you are using a hard disk or a device mimicking a hard disk, such as CompactFlash, in your production system, this boot setup is probably the best choice.

Because this is a well-known and well-documented scheme, we will discuss it only briefly in Chapter 9. You will be able to find a wealth of documentation on this process from various Linux vendors, as well as from online resources.

### Network

In this setup, either the root filesystem or both the kernel and the root filesystem are loaded via a network link. In the first case, the kernel resides on solid-state storage media or a disk, and the root filesystem is mounted via NFS. In the second case, only the bootloader (perhaps a very minimal bootloader, with just enough support to load a kernel image over a local network connection) resides on a local storage media. The kernel is then downloaded via TFTP, and the root filesystem is mounted via NFS. To automate the location of the TFTP server, the bootloader may also use BOOTP/DHCP. In that case, the target does not need any preset IP addresses to find either the TFTP server or the NFS server.

This setup is ideal in early stages of development or during debugging because it enables the developer to share data and software rapidly between his workstation and the target without having to reprogram the target. Software updates can then be compiled on the host and tested immediately on the target. In contrast, few production systems use this setup, because it requires the presence of a server. In the case of the control systems described in Chapter 1, however, this setup actually can be used for some of the devices, because the SYSM module already provides network services.

Obviously, this setup involves configuring the server to provide the appropriate network services. We discuss the configuration of these network services in Chapter 9.

## System Memory Layout

To best use the available resources, it is important to understand the system’s memory layout, and the differences between the physical address space and the kernel’s virtual address space.[^1] Most importantly, many hardware peripherals are accessible within the system’s physical address space, but have restricted access or are completely “invisible” in the virtual address space.

To best illustrate the difference between virtual and physical address spaces, let’s take a look at an example. The venerable HP iPAQ remains popular with some embedded Linux enthusiasts, and is now cheaply available on eBay. Since its memory layout is fairly typical of many devices available, we’ll use it as an example in Figure 2-6.

The physical map of a system is usually available with the technical literature accompanying your hardware. In the case of the iPAQ, the SA-1110 Developer’s Manual is available on Intel’s website.

The physical map is important because it provides you with information on how to configure the kernel and how to develop custom drivers. During the kernel’s configuration, for instance, you may need to specify the location of the flash devices in your

[^1]: What we call here a “virtual address” is known in x86 jargon as a “logical address” and can have other names on other architectures.
