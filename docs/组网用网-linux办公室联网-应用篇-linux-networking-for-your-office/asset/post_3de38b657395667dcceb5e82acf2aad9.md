
(http://www.suse.com) develops many of the cutting-edge XFree86 drivers, so you might find an experimental driver there for a relatively new video board. If you find that you're in possession of an extremely new and unsupported board, it's possible that the Xi Graphics (http://www.xig.com) Accelerated X server supports your board; but purchasing this software might be more expensive than buying a replacement video card.

Video boards, like many computer components, have their own memory. This memory is used to hold the contents of the screen, and sometimes to help with 3D rendering or other features. As you increase the resolution and color depth of your display, you increase the amount of memory required on the video board. You can compute the amount required to run the board at any given resolution with the following formula:

M = x × y × d / 8,388,608

In this equation, M is the memory in megabytes, x and y are the x and y resolutions, and d is the color depth (for instance, 16 for 16-bit color, capable of displaying 65,536 colors). Most video cards on the market today have more than enough RAM to handle a display of 1024×768 or even 1600×1200 at 16-bit, and often at 24-bit or 32-bit. Keep in mind that the speed of the display drops as the screen resolution, and especially the color depth, increases.

## Sound Cards

In general, you don't need a sound card for a server. If you want one nonetheless, you should know that there are three major sources of drivers for sound cards in Linux:

- The Linux kernel—The kernel includes a set of drivers for a number of sound cards. Many of these are older ISA designs, but some are newer PCI cards.
- The OSS drivers—4Front Technologies (http://www.4front.com/) offers the commercial Open Sound System (OSS) drivers for Linux. These drivers are related to the drivers in the Linux kernel, but are available only for a fee.
- The ALSA drivers—The Advanced Linux Sound Architecture (ALSA; http://alsa.jcu.cz/) project is working on a new sound model for Linux, and has a set of drivers available.

Linux sound driver development and the sound card marketplace both change rapidly, so it's difficult to make definite recommendations. ISA boards based on assorted Crystal Semiconductor chipsets are well supported, however, under all three driver sets, and PCI boards based on the S3 SonicVibes chipset are also popular.

## Additional Printer Ports

If you intend to set up a Linux box as a print server, you might find that you want to serve more than one printer from a single computer. Because most printers come with parallel ports, and because most motherboards have only one parallel port, you might need to add one or more parallel ports to your computer. ISA boards to do this are common, and may contain one or two ports. Linux should have no problem using such ports, assuming that you configure the board properly. Where your first parallel port is /dev/lp0, the second is /dev/lp1 and the third is /dev/lp2.

It’s difficult to use more than three parallel ports on a standard Intel-architecture machine. Therefore, you might want to look into using a serial port for further printers, either with a printer that accepts serial input or with a parallel-to-serial adapter. Printing via a serial port is typically slower than via a parallel port, however.

The Universal Serial Bus (USB) is another method of attaching a printer. USB support was added to the Linux kernel with version 2.2.8, but was still quite crude at that time. You can find more information on the state of USB support for Linux at http://peloncho.fis.ucm.es/~inakiy/usbdb-www/. USB is becoming a common interface for printers, especially for inkjets, and in theory you can attach several dozen USB printers to a single computer, so when this technology matures it might be quite useful to Linux users.

Finally, if no other options are available, you can purchase dedicated Ethernet print servers or, for some printers, install an Ethernet board in the printer. These devices make one or more printers directly available on your network. In many cases, using such a server obviates the need for using Linux as a print server. If you want to use Ghostscript in Linux to convert PostScript into the printer’s native format, however, you still need to configure a printer queue and serve that in the usual way. This sort of configuration increases the traffic on your network because the file goes first to your Linux print server and then to the printer itself.

## Backup Hardware

Murphy’s Law guarantees that at least one of your network’s computers will crash catastrophically, taking its operating system and perhaps user data with it. That’s why you should look into using your Linux box as a backup server, using media such as a tape drive for backups. To do this, however, you need appropriate backup hardware, as described in the following sections.

## Tape

One of the most popular backup media is tape. Tape drives come in four major types of interface: SCSI, EIDE/ATAPI, floppy, and parallel port. For serious server use, I recommend a SCSI tape unit. These drives tend to be the most reliable, and they’re available in some of the
