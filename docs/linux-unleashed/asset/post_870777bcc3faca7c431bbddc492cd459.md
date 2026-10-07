
Linux system, including development tools and X, you should provide at least 250MB just for the files. On top of these values, add whatever space is required for your personal files and temporary storage by Linux. A good rule of thumb is to double the space requirements.

On top of the user space, remember to leave room for the swap space. Although the swap space size depends on the purpose and use of the system, a good number to use is 40MB to 64MB.

More than one drive can be used, although a Linux partition should be placed on the first drive. If you need it, DOS and Windows must be loaded on the first drive, as well, because partitions can be placed on other drives if necessary. The number of drives supported depend on the drive controller and BIOS. IDE systems are usually limited to two drives, while EIDE can handle four drives. ESDI and RLL controllers are usually limited to two drives. SCSI controllers can handle up to seven drives per controller (15 with the newer SCSI standards), and several controllers can be located in a single system. SCSI is the most versatile (and also the most expensive) system.

Because hard disks are now inexpensive, obtaining large-capacity drives is relatively easy. Linux can share a disk with up to three other operating systems (and even more with a few tricks), so if you plan to load DOS, Windows 95, and Linux, for example, allocate enough space for each operating system when loaded.

## Video System

Linux can use almost any video card that works without special drivers under DOS and Windows. This includes CGA, EGA, VGA, and Super VGA, as well as Hercules video cards. Some enhanced resolution cards are also supported under Linux, such as the Cirrus Logic, Diamond, ATI, and Trident cards. Since there are hundreds of video cards available, though, there are not enough drivers for all models and special video modes. Because most cards support default VGA and SVGA modes, these can be used in almost every case.

X imposes its own video card requirements, which require bitmap capabilities of a high-resolution card. Although X can run on a VGA or SVGA system, for optimum results a high-resolution card is required. For this reason, make sure that a video driver is available for Linux before purchasing a new video card or that it is compatible with an older card that works with a driver already in existence.

## Mouse

Linux doesn’t use the mouse for character-based sessions, but it is necessary for X. Linux handles practically every type of mouse and trackball that has DOS or Windows drivers. This includes the Microsoft, Logitech, Mouse Systems, and other vendors as well as compatibles. The bus and serial-port mouse are both supported.

Some other pointing devices such as pens, as well as some joysticks used for cursor movement, are supported.

## Tape Drives

Any SCSI tape drive that has a controller recognized by Linux is usable. There are other tape drives that use a proprietary interface which requires a dedicated hardware card. In most cases, if the IRQ, DMA, and memory address can be configured into Linux, the tape drive will be accessible.

Some QIC and similar small-cartridge drives are becoming popular, driven either by the floppy controller card or the parallel port. Drivers for some of these tape drives are available, although not all are supported. Since many of these small QIC drives rely on proprietary compression schemes to boost data density on tapes, you may not be able to write more than the raw cartridge capacity to these drives.

## CD-ROM

Because most CD-ROMs use either a SCSI or EIDE interface, you will need either a SCSI or EIDE controller card. Older CD-ROM drives used to be driven by a variety of cards, such as sound boards. For these, you need a suitable Linux driver. SCSI-based CD-ROM drives will be recognized and supported by Linux as long as the SCSI controller card is recognized.

Linux can’t read all formats of CD-ROMs. At present, it handles only ISO-9660 format file systems. Although ISO-9660 is widely used, not all CD-ROMs are written using it so don’t be surprised if a DOS or Macintosh CD-ROM cannot be mounted properly.

## Removable Media

Removable media support in Linux depends on the type of interface used by the media. Most SCSI-based systems (such as Iomega’s Jaz and SCSI ZIP drives, as well as SyQuest SCSI cartridges) can be used, although the changing of media while a file system is loaded is seldom properly supported. Iomega’s Bernoulli systems and LaserSafe Pro magneto-optical cartridge systems can all be used with Linux without special drivers, as long as the cartridges can be formatted. Some other magneto-optical and removable magnetic media systems will also function properly.

Some removable media requires special drivers, especially those which do not use SCSI but rely on a dedicated hardware card. There is very limited support in Linux for these devices; what is there is mostly provided by programmers who have written a driver for their own use and then made it public domain.

## Printers

Practically all parallel and serial port printers are widely supported as nonintelligent devices. Some drivers are available for specific popular printers, such as the Hewlett-Packard LaserJets and DeskJets, although there are many printers that do not have dedicated drivers yet. If no driver exists for your printer, it will behave as an ASCII-only device.

You can often program your own interface to nonsupported printers by writing a translation table or device driver.

## Modems

Linux supports most serial asynchronous modems, as well as some synchronous devices. Support for ISDN modems is also available as well. As a general rule, if DOS and Windows can use the modem, so can Linux.

Linux supports all baud rates, including the newer compression schemes such as 56K systems with some driver installation. More than one modem is supported on the system. Indeed, you can hang as many modems off a Linux system as you have serial ports.

## Terminals

Linux supports character-based terminals connected through a serial port or a multiport card. Most existing character-based terminals can be used, and any terminal for which you have the control codes can be added. Graphics terminals, in the UNIX sense, use simple ASCII graphic characters and are not X-capable.

X terminals are supported although not all X terminals work properly. X terminals typically need a high-speed connection to properly display graphics (either through a serial port or from a network port). A PC running X client software can function as an X terminal, as well.

## Multiport Cards

Some UNIX-based multiport cards will work with Linux because drivers have been released either by the vendor or users. Before purchasing a multiport card, though, check the availability of drivers. Some multiport cards offer expansion parallel ports as well as serial ports, and these will also need drivers.

Some multiport cards can be connected through a SCSI controller card instead of built as a dedicated card that plugs into an expansion slot. Even SCSI-based expansion cards will need a driver for Linux to use them properly. Network-based multiport cards, including remote access servers, often work without special drivers because each port on the card behaves like a network device.

## Network Cards

Since Linux is a UNIX system, its primary network protocol is TCP/IP. Other protocols can be used with Linux, but because TCP/IP is included with each Linux software package and is the default network protocol, it is the most widely used. TCP/IP's role as the protocol of the Internet also makes it popular. TCP/IP is usually used over Ethernet networks, so most networking systems in Linux are designed around Ethernet.

Many Ethernet network interface cards (NICs, also called network adapters) are available. The most popular Ethernet cards from 3Com, Novell, Western Digital, Hewlett-Packard, and Intel all work cleanly with Linux. Many compatible Ethernet NICs from other vendors also function properly.

## Copyrights

Just because Linux is distributed free, it doesn't mean the software is not copyrighted. Linux is copyrighted under the GNU General Public License (GPL) which is known in the programming community as a “copyleft” instead of “copyright” because it allows you to redistribute the Linux software to anyone who wants it, along with the complete source code. However, the original owner of the components retains the copyrights to the software.

There is no warranty of any kind with Linux. Even if you buy the Linux software from someone and pay them for maintenance, you cannot ever deal with the Linux programmers themselves. They make no statement of functionality at all. If Linux destroys all your accounting data, for example, it's tough luck. You assume the risk. However, it's also true that Linux has proven itself very stable and there are no incidents of serious data damage that were not caused by user error! Another way of looking at the issue is
