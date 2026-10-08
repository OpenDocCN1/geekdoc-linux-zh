
- **Loadable Module Support** In most cases, you should make sure your kernel can load modules. Click the Loadable Module Support button to display a listing of several module management options. Make sure Enable Loadable Module Support is marked Yes. This feature allows your kernel to load modules as they are needed. Kernel Module Loader should also be set to Yes, because this allows your daemons, such as your Web server, to load any modules they may need.

- **Processor Type And Features** The Processor Type And Features window enables you to set up support for your particular system. Here, you select the type of processor you have (486, 586, 686, Pentium III, Pentium IV, and so forth), as well as the amount of maximum memory your system supports (up to 64GB with the 2.4 kernel).

- **General Setup** The General Setup window enables you to select general features, such as networking, PCI BIOS support, and power management, as well as support for ELF and a.out binaries. Also supported is *sysctl* for dynamically changing kernel parameters specified in the */proc* files. You can use redhat-config-proc (the Kernel Tuning tool in the System Tools menu) to make these dynamic changes to the kernel. In the additional device driver support menu, you can enable specialized features like Crypto IP Encapsulation (CIPE) and accelerated SSL.

- **Block Devices (Device Drivers)** The Block Devices window lists entries that enable support for your IDE, floppy drive, and parallel port devices. Special features, such as RAM disk support and the loopback device for mounting CD-ROM image files, are also there.

- **Multi-Device Support (RAID and LVM) (Device Drivers)** The Multi-Device Support window lists entries that enable the use of RAID devices. You can choose the level of RAID support you want. Here you can also enable Logical Volume Management support (LVM), which lets you combine partitions into logical volumes that can be managed dynamically.

- **Networking Options (Device Drivers/Networking Support)** The Networking Options window lists an extensive set of networking capabilities. The TCP/IP Networking entry must be set to enable any kind of Internet networking. Here, you can specify features that enable your system to operate as a gateway, firewall, or router. Network Packet Filtering enables support for an IPtables firewall. Support also exists for other kinds of networks, including AppleTalk and IPX. AppleTalk must be enabled if you want to use NetTalk to connect to a Macintosh system on your network (Filesystems).

- **ATA/IDE/MFMM/RLL Support (Device Drivers)** In the ATA/IDE/MFMM/RLL Support window, you can click the “IDE, ATA, and ATAPI Block Device” button to open a window where you can select support for IDE ATA hard drives and ATAPI CD-ROMS.

- **SCSI Support (Device Drivers)** If you have any SCSI devices on your system, make sure the entries in the SCSI Support window are set to Yes. You enable support for SCSI disks, tape drives, and CD-ROMS here. The SCSI Low-Level Drivers window displays an extensive list of SCSI devices currently supported by Linux. Be sure the ones you have are selected.

- **Network Device Support (Device Drivers/Networking Support)** The Network Device Support window lists several general features for network device support. There are entries here for windows that list support for particular types of network devices, including Ethernet (10 or 100Mb) devices, token ring devices, WAN interfaces, and AppleTalk devices. Many of these devices are created as modules you can load as needed. You can elect to rebuild your kernel with support for any of these devices built directly into the kernel.

- **Multimedia Devices (Device Drivers)** Multimedia devices provide support for various multimedia cards as well as Video4Linux.

- **File Systems** The File Systems window lists the different types of file systems Linux can support. These include Windows file systems such as DOS, VFAT (Windows 95/98), and NTFS, as well as CD-ROM file systems such as ISO and UDF. Network file systems such as NFS, SMB (Samba), and NCP (NetWare) are included, as well as miscellaneous file systems such as HFS (Macintosh).

- **Character Devices (Device Drivers)** The Character Devices window lists features for devices such as your keyboard, mouse, and serial ports. Support exists for both serial and bus mice.

- **Sound (Device Drivers)** For the 2.4 kernel, the Sound window lists different sound cards supported by the kernel. Select the one on your system. For older systems, you may have to provide the IRQ, DMA, and Base I/O your sound card uses. These are compiled as separate modules, some of which you could elect to include directly in the kernel if you want. For the 2.6 kernel, you can select the Advanced Linux Sound Architecture sound support, expanding it to the drivers for particular sound devices (the Open Sound System is also included, though deprecated).

- **Bluetooth Devices (Device Drivers/Networking Support)** Support is here for Bluetooth-enabled peripherals, listing drivers for USB, serial, and PC card interfaces.

- **Kernel Hacking** The Kernel Hacking window lists features of interest to developers who work at the kernel level and need to modify the kernel code. You can have the kernel include debugging information, and also provide some measure of control during crashes.

Once you set your options, save your configuration. Selecting the Save entry on the File menu overwrites your .config configuration file. The Save As option lets you save your configuration to a particular file.

## Compiling and Installing the Kernel

Now that the configuration is ready, you can compile your kernel. You first need to generate a dependency tree to determine what part of the source code to compile, given your configuration. Use the following command in the kernel source directory:

```
make dep
```

You also have to clean up any object and dependency files that may remain from a previous compilation. Use the following command to remove such files:

```
make clean
```

You can use several options to compile the kernel (see Table 33-1). The **bzImage** option simply generates a kernel file called **bzImage** and places it in the **arch** directory. For Intel and AMD systems, you find **bzImage** in the **i386/boot** subdirectory, **arch/i386/boot**. For a kernel source, this would be in **arch/i386/boot**.

```
make bzImage
```

The options in Table 33-1 create the kernel, but not the modules—those features of the kernel to be compiled into separate modules. To compile your modules, use the **make** command with the **modules** argument.

```
make modules
```

To install your modules, use the **make** command with the **modules_install** option. This installs the modules in the **/lib/modules/version-num** directory, where *version-num* is the version number of the kernel. You should make a backup copy of the old modules before you install the new ones.

```
make modules_install
```

The **install** option both generates the kernel files and installs them on your system as **vmlinuz**, incorporating the **make bzImage** step. This operation will place the kernel files such as **bzImage** in the **/boot** directory, giving them the appropriate names and kernel version numbers.

```
make install
```

| Option | Description |
|---|---|
| **zImage** | Creates the kernel file called **zImage** located in the **arch** or **arch/i386/boot** directory. |
| **install** | Creates the kernel and installs it on your system. |
| **zdisk** | Creates a kernel file and installs it on a floppy disk (creates a boot disk, 1.44MB). |
| **bzImage** | Creates the compressed kernel file and calls it **bzImage**. |
| **bzdisk** | Creates the kernel and installs it on a floppy disk (creates a boot disk). Useful only for smaller kernel builds, 1.44MB. |
| **fdimage** | Creates floppy disk image with the kernel, 1.44MB (bootable). |
| **fdimage288** | Creates floppy disk 2.88 image with the kernel (bootable). |

**TABLE 33-1** Compiling Options for Kernel make Command
