# Chapter 3 Booting and Shutting Down

# 3.2 BOOTING PCs

At this point we've seen the general outline of the boot process. We now revisit several of the most important (complicated) steps and discuss the details relevant to Intel systems.

PC booting is a lengthy ordeal that requires quite a bit of background information to explain. When a machine boots, it begins by executing code stored ROMs. The exact location and nature of this code varies, depending on the type of machine you have. On a machine designed explicitly for UNIX or proprietary operating system, the code is typically firmware that knows how to use the devices connected to the machine, how to talk to the network on a basic level, and how to understand disk-based filesystems. Such intelligent firmware is convenient for system administrators. For example, you can just type in the filename of a new kernel, and the firmware will know how to locate and read that file.

On PCs, the initial boot is generally called a BIOS (Basic Input/Output System), and it is extremely simplistic compared to the firmware of a proprietary workstation. Actually, a PC has several levels of BIOS: one for the machine itself, for the video card, and for the SCSI card if the system has one, and sometimes components for other peripherals as network cards.

The built-in BIOS knows about some of the devices that on the motherboard, the IDE and SATA controllers (and disks), network interfaces, power and temperature meters, and system hardware. SCSI cards are usually aware of the devices that are connected to them. Frankly, the complex interactions needed to make these devices work together have been standardized in the past few years, and little manual intervention is required on current systems.

The BIOS normally lets you select which devices the system to try to boot from. You can usually specify an ordered list of preferences such as “Try to boot from a DVD, a USB drive, the hard disk.” Network booting with PXE (see Netbooking PCs on page 363) is also a common option.

Once the BIOS has figured out which device to boot from, it tries to read the first block of the device. This 512-byte segment is the master boot record or MBR. The MBR contains a program that tells the computer from which partition to load a secondary boot program, the “boot loader.” For more information on PC-style disk partitions and the MBR, refer to Chapter 8, Storage.

The default MBR contains a simple program that tells the computer to get its boot loader from the first partition on the disk. Some systems offer a more sophisticated MBR that knows how to deal with multiple operating systems and kernels. Once the MBR has chosen a partition to boot from, it tries to load the boot loader specific to that partition. This loader is then responsible for loading the kernel.