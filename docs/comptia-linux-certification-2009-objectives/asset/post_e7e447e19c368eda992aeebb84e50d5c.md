
Example:

![](img/477ccb2f05b6ba1b2d563ea74f18c197_832_0.png)

Figure 17-3: The function of a bootloader.

### Bootloader Components

The bootloader uses three main components that work together to systematically load the operating system in stages.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_832_1.png)

Bootloader Components

| Component | Description |
| :--- | :--- |
| Boot sector program | It is the first component of the bootloader. It is loaded by BIOS on startup and has a fixed size of 512 bytes. Its main function is to load the second stage bootloader; however, it can also load another sector or a kernel. |
| Second stage bootloader | It loads the operating system and contains a kernel loader. |
| Bootloader installer | It controls the installation of disk sectors and can be run only when booting from a disk. It coordinates the activities of the boot sector and the bootloader. |

### Types of Bootloaders

There are different types of bootloaders in Linux. Some of the bootloaders are described in the following table.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_832_2.png)

Types of Bootloaders

| Bootloader | Description |
| :--- | :--- |
| GRUB | A popular Linux bootloader that allows you to place specific instructions in MBR. |
| LILO | A Linux bootloader that enables you to boot from up to 16 different configuration images, including DOS, OS/2, Windows NT, UNIX, and Linux partitions. |
| ELILO | A bootloader for Unified Extensible Firmware Interface (UEFI) machines. It supports flexible local booting from a FAT-32 filesystem and a wide variety of boot options via network booting over DHCP/TFTP. |
| *Loadlin* | A bootloader that provides an alternative to LILO for users with hardware configurations incompatible with LILO. Unlike LILO, loadlin is a DOS application program that requires the user to first boot into DOS (or Windows) to run Linux. Loadlin starts a logical reload of your system, causing DOS to be completely overlaid with the Linux operating system. |
| *System Commander* | A third-party bootloader that can also be used as a boot manager. This utility enables you to control the environment you boot into, similar to LILO and loadlin. It has a full-featured boot manager and partitioning software. |
| *SysLinux* | An MS-DOS program that is similar to loadlin, although not as suitable as a general purpose bootloader. It is sometimes used to simplify a first-time installation of Linux and for creating a rescue boot disc. |

### GRUB Loading Order

GRUB loads in the following order: the primary bootloader is loaded, followed by the secondary bootloader and finally, the operating system is loaded. After receiving the correct instructions for the operating system to start, GRUB locates the boot file and hands off control of the machine to that operating system.

### The LILO Boot Process

LILO boots itself in two stages, each of which is composed of several smaller processes. As the boot process progresses, additional letters of the four-letter prompt are displayed. When LILO has fully loaded itself, it displays the LILO: prompt.

During the first stage of boot, LILO moves itself into a memory address and sets up the stack. It then loads the secondary bootloader and transfers control to it. Once the secondary bootloader starts, it continues with the boot process and displays the LILO: prompt.

If LILO does not successfully load, it will freeze at a certain point in its display. The following table shows each step of the display and boot process.

| LILO Display | First Stage Bootloader | Second Stage Bootloader | Description |
| :--- | :--- | :--- | :--- |
| L error | Loaded | Cannot be loaded. | A two-digit error code is displayed. |
| LI | Loaded | Loaded but could not execute. | This is often caused by a geometry mismatch. |
| LIL | Loaded | Started but cannot load descriptor table. | This is often caused by a media failure or geometry mismatch. |

### Benefits of LILO

LILO does not depend on a specific filesystem. It can boot Linux kernel images from floppy disks and hard disks and can even boot other operating systems. One of up to 16 different images can be selected at boot time. Various parameters, such as the root device, can be set independently for each kernel.

LILO can even be used as MBR. MBR is the first sector of your hard disk. The computer’s BIOS looks up to MBR for instructions on how to load an operating system. If you just had Windows 95 or DOS installed, it will only contain instructions to load that one operating system.

## LILO Configuration File

Settings for LILO are saved in the /etc/lilo.conf file. When you boot your system, LILO uses the information in this file to determine how to boot your system.

## UEFI

Earlier known as Extensible Firmware Interface (EFI), UEFI specifies an interface that operates between the operating system and the platform firmware. It is an alternative to BIOS for initiating a system, but does not completely replace BIOS.

## The Boot Process

![](img/477ccb2f05b6ba1b2d563ea74f18c197_834_0.png)

The *boot process* is a process that is repeated each time your computer is started, by loading the operating system from your hard drive. It involves a series of sequential steps. The boot sequence can be divided into the BIOS initialization, bootloader, kernel and init initialization, and boot scripts.

The boot process consists of the following stages:

- 1. The processor checks for the BIOS program and executes it.
- 2. BIOS checks for peripherals, such as floppy disk drives, CD-ROMs, and the hard disk, for bootable media. It locates a valid device to boot the system.
- 3. BIOS loads the primary bootloader from the MBR into the memory. The bootloader is a program that contains instructions required to boot a machine. It also loads the partition table along with it.
- 4. The user is prompted with a graphical screen that displays the different operating systems available in the system to boot from. The user should select an operating system and press **Enter** to boot the system. If the user does not respond, then the default operating system will be booted.
- 5. The bootloader determines the kernel and locates the corresponding kernel binary. It then uploads the respective initrd image into the memory and transfers the control of the boot process to the kernel.
- 6. The kernel configures the available hardware, including processors, I/O subsystems, and storage devices. It decompresses the `initrd` image and mounts it to load the necessary drivers. If the system has implemented any virtual devices such as LVM or software RAID, then they are initialized. The components that are configured by the kernel will be displayed one by one in the screen.
- 7. The kernel mounts the root partition and releases the unused memory. To set up the user environment, the `init` program is executed.
- 8. The init program searches for the `initab` file, which contains the details of the runlevel, that has to be started. It sets the environment path, checks the filesystem, initializes the serial ports, and runs background processes for the runlevel.
- 9. If the graphical mode is selected, then `xdm` or `kdm` is started and the login window is displayed on the screen.
- 10. The user enters the user name and password to log in to the system.
- 11. The system authenticates the user. If the user is a valid user, then the profile, the `.login`, the `.bash_login`, and the `.bash_profile` files are executed. The shell is started and the system is ready for the user to work on.

`xdm` refers to the X Window Desktop Manager. Users who use GNOME or KDE, use either `gdm` or `kdm`, respectively. In RHEL 5.3, `gdm` is the default desktop manager.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_835_0.png)

## Superblocks

**Definition:**

A *superblock*, often called sb, is a data structure that is stored on a disk and contains control information for a filesystem. Linux partitions are discussed in terms of blocks. The superblock comprises the first 512 bytes of a partition. It contains information about the block size used by the filesystem, the location of the root directory, and the time it was last checked.

Each partition on a disk is identified by a number. The number 1, is assigned to the first partition, number 2, to the second partition, and so on.
