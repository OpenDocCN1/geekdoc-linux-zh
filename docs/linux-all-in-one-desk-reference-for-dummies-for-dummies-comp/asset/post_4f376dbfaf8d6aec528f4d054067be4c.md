
# Floppy Tape Support

- `Ftape, the floppy tape device driver`
- `Ftape (I2C-80/Trawian) support` `[F_TAPE]` `[N/m/y/?]`

You can also enable several parameters related to floppy tape drives.

## Advanced graphics support

The next set of options configures support for advanced video cards that can perform hardware-accelerated, 3-D graphics. You can enable the first option to build the AGP (Accelerated Graphics Port) driver and can answer `Yes` to the option for your specific chipset.

`/dev/agpgart` `[AGP Support]` `[AGP]` `[Y/m/n/?]`

Next, you have to configure a set of options for the Direct Rendering Manager (`DRM`)—a device-independent driver that supports the `XFree86 Direct Rendering Infrastructure` (`DRI`). `DRI` is meant for direct access to 3-D graphics hardware in advanced graphics cards, such as `3Dfx Banshee` and `Voodoo3+`. To find out more about `DRI`, use the Web browser to visit the URL `http://dri.freedesktop.org/wiki`.

If you have a 3-D graphics card, you can answer `Yes` to `DRM` and build the module for the graphics card in your system. If you do not have one of the listed graphics cards, you should answer `No` to these options.

## I2C Support

`I2C (Inter-Integrated Circuit)—pronounced EYE-squared-see—is a protocol Philips has developed for communication between integrated circuit chips over a pair of wires at rates between 10 and 100 kHz. System Management Bus (SMBus) is a subset of the I2C protocol. Many modern motherboards have an SMBus meant for connecting devices such as EEPROM (electrically erasable programmable read only memory) and chips for hardware monitoring. Linux supports the I2C and SMBus protocols. You need this support for video for Linux. If you have any hardware sensors or video equipment that needs I2C support, answer `m` (for module) to the I2C Support option and answer `m` for the specific driver for your hardware. For example, if you want to use a BT848 frame-grabber board (to capture video), you should answer `m` to `I2C, I2C_ALGOBIT,` and `VIDEO_BT848` options (the `I2C_ALGOBIT` option enables support for what is known as the `I2C bit-banging` interface that the `BT848 board` supports).

## Multimedia devices

This category of options configures support for multimedia devices such as video cameras, television tuners, and FM radio cards.

# Rebuilding the Kernel

## Frame buffer

Through these options you can enable support for frame-buffer devices. A frame buffer is an abstraction for the graphics hardware so that the kernel and other software can produce graphical output without having to rely on the low-level details (such as hardware registers) of a video card. Frame buffer support is available for many video cards.

## Sound

Use this set of options to configure sound card support. If you have a sound card installed, start by answering m to the Sound Card Support option. After that, answer m for Advanced Linux Sound Architecture (ALSA) and the sound devices. You can always build the sound modules for all types of sound cards. That way, the modules needed for your system's sound card are available when needed.

## USB support

Use this category of options to configure support for the Universal Serial Bus (USB) — a serial bus that comes built into most new PCs. USB version 1.1 supports data-transfer rates as high as 12 Mbps — 12 million bits per second or 1.5MB per second — compared with 115 Kbps or the 0.115 Mbps transfer rate of a standard serial port (such as COM1). You can daisy chain up to 127 devices on a USB bus. The bus also provides power to the devices, and you can attach or remove devices while the PC is running — a capability commonly referred to as hot swapping or hotplugging. USB version 2.0 (or USB 2.0 or USB2, for short) ups the data-transfer ante to 480 Mbps, slightly faster than the competing IEEE 1394 (FireWire) bus.

USB can replace the functionality of the PC's serial and parallel ports, as well as the keyboard and mouse ports. Nowadays, many PC peripherals — such as the mouse, keyboard, printer, scanner, modem, digital camera, and so on — are designed to connect to the PC through a USB port.

If your PC has a USB port, answer m to the Support for USB option (so that a module is built). Then you have to answer n to the EHCI_HCD, UHCI_HCD, or OHCI_HCD option, depending on the type of USB interface — EHCI (for USB 2.0), UHCI (Intel) or OHCI (Compaq and others) — your PC has. To determine the type of USB interface, type lspci in a terminal window and look for the USB controller's make and model in the output.

For USB 2.0 support, you can answer m to the EHCI_HCD (that's host controller device) option.

After you select the UHCI or OHCI interface support, you have to build the driver modules for specific USB devices on your system.

## File systems

Through this category of options, you can turn on support for specific types of file systems. You’d be amazed by the many different file systems that the Linux kernel can support. (Table 5-1 lists just some of them.) You typically build a kernel with support for the core Linux file systems (Ext2 and Ext3), CD-ROM file system (ISO 9660 and Joliet), and DOS/Windows file systems (MSDOS, FAT, and VFAT). For sharing files with Windows 2000/XP systems, you also build the module for CIFS.

**Table 5-1 Some File Systems Supported by the Linux Kernel**

| File System | Description |
| :--- | :--- |
| Apple Macintosh | The Macintosh HFS file system. (Linux can read and write Macintosh- formatted floppy disks and hard drives.) |
| CIFS | The Common Internet File System (CIFS) — a successor to the Server Message Block (SMB) protocol — is the new file system for Windows servers such as Windows 2000, Windows XP, and Samba. |
| Coda | An advanced network file system that is similar to NFS but that better supports disconnected operation (for example, laptops) and is a better security model |
| Ext2 | The second extended file system — the current standard file system for Linux |
| Ext3 | Ext2 file system with support for journaling — a facility that allows quick recovery of the disk after a crash |
| FAT | Refers to any File Allocation Table (FAT)-based file system (including MS-DOS and Windows 95 VFAT file systems) |
| HPFS | The OS/2 HPFS file system. (Linux can only read HPFS files.) |
| ISO 9660 | The standard ISO 9660 file system used on CD-ROMs. (This system is also known as the *High Sierra File System* and is referred to as `hfs` on some UNIX workstations.) |
| Joliet | Microsoft’s Joliet extension for the ISO 9660 CD-ROM file system, which allows for long filenames in Unicode format. (Unicode is the new 16-bit character code that can encode the characters of almost all languages of the world.) |
| Minix | The Minix file system — the original file system of Linux |
| MSDOS | The MS-DOS file system |
| NFS | Network File System for sharing files and directories from other systems on a network |
| NTFS | NT file system (NTFS) — the file system used by Microsoft Windows NT and XP. (Linux can only read NTFS disks.) |
| /proc | A virtual file system through which you can get information about the kernel. The `/proc` file system does not exist on the disk; files are created when you access them. |
| ReiserFS | An efficient file system that stores both filenames and files in a balanced tree and uses journaling |
| SMB | File system that uses the Server Message Block (SMB) protocol to access shared directories from networked PCs running Windows 95/98/NT/2000 |
| System V | File system used by SCO, Xenix, and Coherent variants of UNIX for Intel PCs |
| UDF | A new file system used on some CD-ROMs and DVDs. (For example, the UDF file system is used on rewritable CDs written in packet mode or written by UDF utilities such as DirectCD.) |
| UFS | File system used by the BSD (Berkeley Software Distribution) variants of UNIX (such as SunOS, FreeBSD, NetBSD, and NeXTstep). |
| VFAT | Windows 95/98/NT/2000 file systems with long filenames. |

## Partition types

Linux can read and manipulate disk partitions created by many different systems. These options enable you to include support for specific partition types:

- Partition Types
    - Advanced partition selection (PARTITION_ADVANCED) [Y/n/?]
    - Acorn partition support (ACORN_PARTITION) [N/y/?]
    - Alpha OSF partition support (OSF_PARTITION) [Y/n/?]
    - Amiga partition table support (AMIGA_PARTITION) [N/y/?]
    - Atari partition table support (ATARI_PARTITION) [N/y/?]
    - Macintosh partition map support (MAC_PARTITION) [Y/n/?]
    - PC BIOS (MSDOS partition tables) support (MSDOS_PARTITION) [Y/n/?]
    - ... lines deleted ...

## Native language support

This set of configuration options requires you to select a native language character set. The Microsoft FAT file systems use these character sets to store and display filenames in one of several languages. The character sets are stored in files called *DOS codepages*. You have to include the appropriate codepages so that the Linux kernel can read and write filenames correctly in any DOS partitions on the hard drive. Note that the codepages apply only to filenames; they have nothing to do with the actual contents of files.

You can include support for as many codepages as you want. Simply answer Yes to the codepages for your selection of languages.
