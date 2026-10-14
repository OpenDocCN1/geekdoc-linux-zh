
- If you intend to create a dual-boot system, you must prepare the hard disk before you start to install Linux. You create partitions for the Linux file system and swap partition using a utility such as parted, FIPS, or PartitionMagic.
- The BIOS controls the boot process by passing control to the MBR, which in turn can contain a Linux boot manager such as GRUB or LILO, or it can pass control on to the boot record of the active partition.
- Many Linux distributions are available, each with a slightly different technical focus and often with different end users as its primary customers. Vendors of commercial distributions try to distinguish their products by offering documentation, technical support, additional software packages, or related services.
- Linux installations are started by a boot disk or bootable CD-ROM, DVD, or USB device. A user defines the source of the Linux files and the target partition where they will be stored. The user also answers a number of questions during the installation process to define exactly what software will be installed and how it will be configured.
- Attractive graphical installation programs are standard in commercial versions of Linux. On many systems a complete Linux installation takes only about 15 minutes plus the time required to copy files to your hard disk.
- You can install Linux from a CD-ROM, from files stored on a hard disk, or across a network connection. The CD-ROM option is most widely used except when Linux is installed on a large number of systems at the same time, in which case a network install is most likely.
- The various components of Linux are sometimes arranged on different hard disk partitions to make system administration tasks easier. You can configure these partitions within the Linux installation program.
- Installation programs generally provide multiple installation types that let you define the sorts of programs you want to install as part of Linux. For example, server, graphical workstation, or software development station might define different sets of applications that are installed with the basic operating system.
- Software packages are managed using special file formats such as the Red Hat Package Manager format (rpm).
- Installing multiple identical systems or reinstalling the same system multiple times can be done more easily using the Kickstart method, which uses a configuration file to hold all installation selections.
- A Kickstart installation uses a text configuration file called ks.cfg. This file is stored on the boot disk. It can be created manually or using the Kickstart Configurator graphical utility.

## COMMAND SUMMARY

No new Linux commands were introduced in this chapter.

## Key Terms

**active partition** — The bootable partition; the partition that the MBR passes control to if the MBR does not itself contain a boot manager.

**BIOS (Basic Input/Output System)** — Information stored in ROM that provides instructions to the operating system for using the devices on a computer.

**bit** — A binary digit; a bit can hold a value of either one or zero.

**block** — A unit of hard disk space; typically one that contains 1024 bytes, or two sectors.

**boot disk** — A removable disk that can start an operating system, especially one that starts a Linux installation program.

**boot manager** — A program that lets you start one or more operating systems each time you start a computer. (Examples include GRUB and LILO.)

**boot record** — A small area on each partition that contains a program to start the operating system on that partition.

**bootable CD-ROM drive** — A CD-ROM drive that can start an operating system (or other program) directly from a CD without accessing the hard disk. (This feature of the CD-ROM drive must be enabled by the BIOS.)

**broadcast address** — An IP address that sends a packet of data to all computers on a network.

**byte** — Storage space sufficient to store one character; eight bits.

**CMOS RAM** — A special memory chip in which computer configuration details are stored. The data is maintained by a tiny battery and is modified as needed using a BIOS utility.

**cylinder** — A set of tracks at the same location on all the platters of a hard disk.

**defragment** — A procedure that arranges each file so that the parts of the file are next to each other on the hard disk; places all sectors composing a file into contiguous disk locations.

**device driver** — Software used to communicate with or control a hardware component.

**direct memory access (DMA) channel** — A communication method within a computer that allows a device to read and write directly to the computer's RAM, without going through the microprocessor first.

**disk image** — A single file that contains an exact copy of a floppy disk.

**domain name** — A name assigned to a collection of computers on a network.

**dual-boot system** — A computer that allows a user to choose which operating system to start each time the computer is started.

**FAT** — (file allocation table) The file system type used by older versions of Windows (such as Windows 3.1).

**FAT32** — (file allocation table, 32-bit) The file system type used by some versions of Windows (such as Windows 98).

**FIPS** — A program that creates two separate partitions from an existing Windows partition. Used to create an empty partition that can be deleted and the resulting free space used for installing Linux. Can not be used with the NTFS file system (Windows NT, 2000, XP, or Server 2003).

gigabyte (GB) — A measure of space on computers equal to 1024 megabytes, or roughly enough space to store 1 billion characters.

GRUB — A Linux boot manager; used by default on Red Hat Linux and Fedora distributions.

hexadecimal (hex) — A numbering system using base 16. Hex uses 0 to 9, plus the letters A through F (usually capitalized) to count the numbers 10 through 15.

I/O ports — Special addresses (resembling memory addresses) used by a device for port-mapped I/O.

IDE — A low-cost, easy-to-manage interface used by most computers to connect hard disks and CD-ROM drives to the CPU.

IDE controller — A hardware component used to communicate between an IDE-compatible hard disk or other IDE device and the microprocessor.

install disk — A disk used to start the Linux installation program on some distributions of Linux. See boot disk.

installation source — The set of files from which Linux is installed. These files are normally stored on a Linux CD-ROM.

installation type — A specification indicating which Linux software to install; the appropriate installation type depends on how the Linux system will be used.

interrupt request (IRQ) — A numbered signal that a device sends to the operating system to request service.

Kickstart — A method of controlling the installation of Red Hat Linux or Fedora using a prebuilt configuration file instead of responding to questions at the keyboard during the installation.

kickstart configuration file — The text file used to control a Kickstart installation, named ks.cfg.

LILO (Linux Loader) — A Linux boot manager.

live CD — A CD-ROM containing a Linux distribution that can be run in computer memory and using the data on the CD-ROM, without ever performing a traditional Linux installation. No information is ever written to the hard disk.

logical partition — A hard disk partition that exists within one of the four partitions that a hard disk can traditionally manage. Logical partitions are numbered beginning with 5. See also primary partition.

Master Boot Record (MBR) — A small area on the first hard disk that contains a program to decide how to start an operating system. Control passes from the BIOS to the program in the MBR when a computer is first booted.

megabyte (MB) — A measure of space on computers equal to 1,048,576 bytes, or enough space to store roughly 1 million characters.

mount point — A subdirectory through which a set of data such as a hard disk partition is accessed.

network address — An address that identifies the local network of which a computer is a part. This address is used to determine how data is routed to its intended destination.

NTFS (NT file system) — The default file system type for Windows NT, Windows 2000, Windows XP, and Windows Server 2003.
