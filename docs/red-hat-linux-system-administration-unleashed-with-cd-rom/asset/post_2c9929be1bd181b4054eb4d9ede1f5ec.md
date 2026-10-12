
Probing of parallel ports is a dangerous proposition and may result in the system locking up. It is much safer to specify port settings, such as addresses and IRQ settings, by specifying these parameters on the boot command line, in lilo.conf, or when loading the parport modules.

The parport module divides the control of the parallel port into two modules, one of which manages the port sharing that is architecture independent and an architecture-dependent module. One or both of these may be compiled as modules.

Again, more documentation of this feature is found in the Documentation directory in the files parport.txt and paride.txt.

Many modern systems, especially laptops and other portables, include support for Advanced Power Management, also known as APM. APM-capable systems have the ability to conserve power by shutting down monitors during periods of inactivity, spinning down and parking hard drives, or suspending the system completely. Unfortunately, each vendor’s implementation of APM differs, making it difficult to support in the kernel. These differences also mean that if you are having problems with your kernel, you should first turn off support for APM and then attempt to reproduce the problem.

There are options in two different places for watchdog systems whose function is to take action in the event the system crashes. Hardware-based watchdog systems are set later on, but in the general options section, you may set support for software-based watchdog systems. With this option set, the kernel will monitor and periodically update /dev/watchdog and if the update fails to occur on schedule, a reboot of the system will be forced. This support is useful if you have systems that are remotely administered and that must be rebooted in the event of a crash.

More information on software and hardware watchdogs can be found in the kernel Documentation tree in the file watchdog.txt.

## Plug-and-Play Support

With recent kernels, some support for plug-and-play devices has been added and in this section of the kernel configuration, you can select whether or not to include it. Read the help information for these options and set them according to your needs.

## Block Devices

The next major subdivision of the kernel configuration contains options to support various block devices. These options include support for IDE/ATAPI devices, parallel port IDE device support, various PCI chipsets, and support for Linux software RAID, which is discussed in detail in Chapter 9, “Linux and RAID.” Let’s take a closer look at a few of these options.

One of the most configurable drivers among the block devices is the floppy disk driver. This driver has the capability to control not only floppy drives, but backup devices as well and it is also capable of running multiple disk controllers. There are a number of command-line arguments that can be passed to the floppy driver either on the kernel command line or via the /etc/lilo.conf file using the append command. Table 35.3 describes a few of these options.

### TABLE 35.3 Floppy Driver Option

| Option | Description |
|---|---|
| floppy=daring | Usable on most modern Pentium systems, this option allows for optimizations that can speed up floppy access, but is not compatible. |
| floppy=one_fdc | This option tells the driver that there is only one controller available. |
| floppy=two_fdc or floppy=<address>, two_fdc | Uses two controllers with the second located at the specified address. |
| floppy=thinkpad | Required for some ThinkPad laptops that invert the convention for the disk change line. |
| floppy=omnibook or floppy=nodma | Prevents the use of DMA for data transfers. Required for some HP Omnibook systems. |
| floppy=yesdma | Used to force DMA mode. This option is the default setting. |
| floppy=nofifo | Use this setting if you receive "Bus master arbitration" errors from the Ethernet card or other devices while using your floppy. |
| floppy=<threshold>, fifo_depth | Sets the FIFO depth for DMA mode. Compiling as a module allows experimentation with this parameter to find optimal settings. |
| floppy=<drive>, <type>,cmos | Sets the CMOS type for the specified drive to the given type. This option is required if you have more than two floppy drives. |
| floppy=broken_dcl | Avoids using the disk change line and assumes that the disk has been changed whenever the device is reopened. Useful for some laptops and older PCs. |
| floppy=L40SX | Prevents printing of messages when unexpected interrupts are received. Required on IBM L40SX laptops to prevent a conflict between the video and floppy disk controllers. |
| floppy=<nr>,irq and floppy=<nr>,dma | Sets the IRQ or DMA channel for the specified device. |
| floppy=slow | Required for some PS/2 machines that have a slower step rate. |

The complete list of floppy module options can be found in README.fd in the /usr/src/linux/drivers/block directory and the fdutils package. A set of floppy driver utility programs, including an enhanced mtools kit, can be downloaded from ftp://metalab.unc.edu/pub/Linux/system/Misc/.

### Tip

The floppy driver options are specified as shown in the preceding table, but unlike many other kernel and module options, you are allowed to make only one such declaration. Therefore, to set multiple options, you must specify them all at one time. For example, to specify the daring and two_fdc to the floppy module, you would issue the following command:

```
insmod 'floppy="daring two_fdc"'
```

You may also pass options to the floppy driver using the append line in the LILO configuration file /etc/lilo.conf, on the kernel command line, or through the older environment variable syntax.

Enhanced IDE Support under Linux is also selected under the block devices option, and in addition to supporting up to eight IDE drives, there is also support for IDE/ATAPI CD-ROM, tape drive, and floppy drives. The new driver in the 2.2 kernel also includes support for the PIO modes on OPTi chipsets, SCSI host emulation, as well as support for a large number of chipsets.

Tuning of the IDE drives is accomplished using the hdparm utility. Additional details on options and tuning is available in the Documentation directory in the ide.txt file.

### Caution

If you are required to pass options to the IDE driver while loading it as a module, you must replace any commas with semicolons in the command line.

```
insmod ide.o options="ide0=serialize ide2=0x1e8;0x3ee;11"
```

## Loopback Devices

Loopback devices allow you to create files and then treat them as a filesystem. For example, you can create an image of a floppy disk or create a CD-ROM image from a filesystem and then use the loopback device to mount it as a regular filesystem and make changes before committing the image to a disk or CD-R. The loopback device is also used in some of the available schemes for encrypting filesystems as outlined in the Loopback Encrypted Filesystem HOWTO, which can be found at http://www.linux.com/Loopback-Encrypted-Filesystem-HOWTO.html. In order to take advantage of the loopback device, you must have an up-to-date util-linux package. To determine the correct version to support your kernel, refer to the Changes file in the /usr/src/linux/Documentation directory.

## Support for Network Block Devices

An experimental option that can be selected under block devices is support for network block devices. Network block devices allow the client system to access a block device on a remote system transparently over TCP/IP. This is different from NFS or Coda in that the block devices accessed in this manner can be used for any type of filesystem, including swap devices.

## Linux Software RAID

One of the major features you can select under block devices is support for software RAID. This software RAID is fully described in Chapter 9 along with utilities required to manipulate RAID arrays under Linux.

## Parallel Port IDE Devices

Support for parallel port IDE devices is included here as well. This option allows you to use devices such as external hard drives and other IDE/ATAPI devices that connect to your computer via the parallel port. One caveat is that if you compile this option as a module, you must also compile the parport option as a module.

## Networking Options

Just like UNIX, Linux is a network operating system and the Linux system that stands alone is rare. Even the workstation in the home office is typically connected to the Internet via the PPP network protocol. A Linux workstation without network services is like a car on blocks. It has a powerful engine and lots of cool buttons and knobs, but...
