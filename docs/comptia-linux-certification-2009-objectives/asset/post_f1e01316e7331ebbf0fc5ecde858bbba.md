
# TOPIC A
## Prepare for Installation

You troubleshoot devices to ensure the smooth operation of the Linux system. To optimize the performance of the Linux system, you need to select devices that are fully supported by Linux. In this topic, you will perform the preparation tasks necessary for a successful installation of Linux.

Preparing for a new Linux installation is much like setting out to cook a fine meal. You need to gather all the necessary ingredients to accomplish the task. Thorough preparation will help prevent failure when attempting to boot your system for the first time.

### Hardware Compatibility

The first thing you should do before purchasing any hardware component is to check whether it is on the hardware compatibility list (HCL) for Linux. Before you install Linux, you should gather information about your system. Much of this information is available in your system documentation. Some of the questions that you should address before purchasing a hardware component are listed in the table below.

| Component | Questions to Address |
| :--- | :--- |
| Hard drive | - How many devices are installed? <br> - Is it IDE or SCSI? <br> - How large is the drive? <br> - How many cylinders are contained on the drive? |
| Hard disk controller | - Is it IDE or SCSI? <br> - Who is the manufacturer? |
| Memory | How much RAM is installed? |
| CD-ROM | Is the interface type IDE, SCSI, or other? (If it is not IDE or SCSI, you will need to record the make and model.) |
| SCSI adapter | - Who is the manufacturer? <br> - What is the model? |
| Network card | - Who is the manufacturer? <br> - What is the model? |
| Mouse | What type is it? (If serial, record the port to which it is connected.) |
| Monitor | - Who is the manufacturer? <br> - What is the model? <br> - What are the horizontal and vertical refresh rate ranges of the monitor? |
| Display adapter | - What chipset is used in the display adapter? <br> - How much video RAM does the display adapter use? |

### Linux Distributor Testing

Distributors, such as Red Hat, Inc., test whether Linux operates correctly with specific hardware. After testing, they produce HCLs for each supported version. The lists include information about the hardware, but because the computer system configurations vary between what you may have and what they tested, the variations in manufacturing specifications aren't guaranteed to be compatible with any hardware. HCL is a list of hardware that has been tested under specific conditions (usually under many conditions) and should be used as a guide, not as an absolute testament that the hardware will work perfectly straight out of the box (because your system is probably configured in a slightly different way than the test systems).

### Hardware Compatibility Websites

The following Linux hardware compatibility sites will assist you in determining if your hardware will work with Linux:

- Red Hat hardware compatibility list—https://hardware.redhat.com/
- Mandriva hardware compatibility list—http://hcl.mandriva.com/
- SuSE hardware compatibility list—http://en.opensuse.org/Hardware
- Fedora hardware compatibility list—http://fedoraproject.org/wiki/HCL
- Ubuntu hardware compatibility list—http://www.ubuntu-hcl.org
- Linux Mint hardware compatibility list—http://www.linuxmint-hcl.org

### CPU Compatibility

It is also important to determine if your CPU is compatible with Linux. Certain distributions of Linux are tailored to different CPU types.

### Installation on New Systems

On newer systems, the Linux installation program often automatically identifies your hardware. It is still a good idea to gather information ahead of time, just in case the program does not figure out what you have.

### Gather Installation Information

Depending on your installed equipment, you may have to look for information in a variety of resources.

- One way to gather information is to view CMOS or diagnostic information available at system boot time. Cold-boot your system and display setup or diagnostic information. This is displayed in different ways on different systems. For example, on most Compaq systems, when the block cursor moves to the upper-right corner of the screen, press F10. On some systems, when the View Setup message (or a similar message) is displayed, you press Delete (or the key indicated in the message).
- Access to manuals that came with the equipment can often be one of the best ways to find out about components. Manufacturers' websites also often contain valuable information about equipment.
- If you don't have the documentation and you don't have an application or a utility to provide this information, you will need to open the hood and look inside. Many cards, boards, and components have manufacturer and model information printed on them. However, they probably will not have a guide to interpreting the jumpers' settings.

If your workstation is to be connected to a network, you will also need information about the network address to be assigned to your computer. Some systems will have a permanent network address and others will obtain a network address each time they access the network. Contact the system or network administrator to find out how to set up your system.

## Linux Installation Methods

![](img/477ccb2f05b6ba1b2d563ea74f18c197_825_0.png)

Linux installation can be done for servers and workstations. There are different methods by which Linux can be installed.

| Installation Method | Description |
|---|---|
| Local CD/DVD-ROM Installation | Linux can be installed from a set of installation CD/DVD-ROMs. It requires the system's BIOS settings to support booting from CD/DVD-ROMs. This is like a local installation and is the easiest way to install Linux. |
| Local Hard Drive Installation | Linux installation can be done by staging the installation files on the local hard drive. |
| USB Drive Installation | Linux can also be installed through USB drives if CD/DVD-ROMs or other modes of installation are not supported by the system. To enable booting from USB drives, the diskboot.img file has to be copied from the images folder of the installation CD/DVD-ROM to the USB drive. This mode of installation also requires the BIOS to support booting from USB drives. |
| Network-Based Installation | Linux installation can be done on networked computers by staging all the installation files on a separate server and installing it on clients' systems. The network installation server shares the installation directory with the clients via NFS, FTP, or HTTP. This method is often faster than CD/DVD-ROM-based installations. The network installation server is necessary for all network-based Linux installations. |

## Preinstall Checklist

1. Collect basic system information about your computer.
2. Check the available hardware with HCL.
3. Verify that the minimum system requirements are met for the distribution you wish to install.
4. Plan the hard disk partitioning layout and the corresponding filesystems, including the size of the swap drive, depending on the physical RAM.
5. If necessary, check the installation media using the Test the Media option available on the Linux Installation CD.

## The Anaconda Installer

The Anaconda installer is an installation program that enables installation of Linux through the text mode or the graphical mode. It provides step-by-step instructions to guide installation. It also enables you to partition and organize hard disks and manage RAID and LVMs. The installer provides various options to choose and add different packages based on your operating requirements.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_826_0.png)
![](img/477ccb2f05b6ba1b2d563ea74f18c197_826_1.png)
![](img/477ccb2f05b6ba1b2d563ea74f18c197_826_2.png)

Figure 17-1: The Anaconda installer in Red Hat Enterprise Linux 5.

## Partitioning Utilities

![](img/477ccb2f05b6ba1b2d563ea74f18c197_826_3.png)

### Definition:

The Linux operating system is usually installed on a partition of the hard disk. A partition utility is a program that is used to manage partitions on the hard disk. A partition utility enables you to create a new partition, modify the attributes of an existing partition, assign a filesystem to a partition, and delete a partition. The utility also enables you to specify the size of a partition and indicate whether the partition is a primary or a logical partition. The most frequently used partition utility is fdisk.

### Example: Disk Druid

Disk druid is a program that is used to partition disk drives during the installation process.
