
software to use the hardware. The second step is to clear disk space for use by FreeBSD. This second step is simplest if you intend to use *only* FreeBSD on the computer. If the system currently runs other OSs, you may need to add a hard disk, shrink existing partitions, or re-allocate partitions for FreeBSD's use.

## Checking Hardware Compatibility

Chapter 1 included a description of some of the major concerns in hardware compatibility. Of the core system components, you should check on the compatibility of SCSI host adapters, network cards, and video cards. All of these components require special FreeBSD drivers (or drivers in tools within FreeBSD, such as *Xfree86*). Most instances of these devices are well supported by FreeBSD, but a few are not. Less critical systems, such as sound cards, video capture cards, internal modems, scanners, and printers also require drivers. Support for these is spottier, but still good for some device types, such as printers and sound cards. For all of these devices, consult the `HARDWARE.TXT` file that comes with FreeBSD to learn about support for specific devices. (This file is also available at <ftp://ftp.FreeBSD.org/pub/FreeBSD/releases/i386/5.0-RELEASE/>)

Some devices are very well standardized, so FreeBSD supports them using its normal drivers, and you don't need to be too concerned about compatibility. These devices include CPUs (within the x86 family, as described in Chapter 1), motherboards, RS-232 serial ports, parallel ports, keyboard ports, PS/2 mouse ports, floppy ports and drives, specific models of hard disk and CD-ROM drives, and to some extent EIDE controllers. EIDE controllers all work alike in their most basic and low-performance modes, but to get better performance, FreeBSD needs special controller-specific drivers. Because EIDE controllers are integrated on modem controller chipsets, this issue is sometimes discussed as if it were a motherboard (or motherboard chipset) issue. In a worst-case scenario, you can add a separate EIDE controller card to work around lack of support for the accelerated modes of an EIDE controller on a motherboard.

If the computer is currently running Windows, you can learn a lot about its device from the Windows Control Panel. Specifically, the System object's Device Manager window (shown in Figure 2-1, from Windows 2000), which is accessible as an option from the Hardware tab, lets you browse through various devices. You may be able to learn the device's manufacturer, the name of the chipset, or the name of the driver. These can be important clues, but they can sometimes be deceptive. For instance, the device manufacturer's name may not be what's important because most FreeBSD drivers are written for the *chipsets* used by the device. (A chipset is one or more chips that provide most of the device's functionality. Many manufacturers use chipsets from other manufacturers.)

Another way to learn about your computer's hardware is to examine the chips yourself. Look at the largest chip. This probably bears a manufacturer's name or logo and a model number, as shown in Figure 2-2. This figure shows the main chip on a Matrox Millenium video card, clearly identifying it as using a Matrox MGA 2064W

![](img/f34d37e3abe9f4517128e54f80ab2616_75_0.png)

**Figure 2-1.** The Windows Device Manager window can help you learn about your computer prior to installing FreeBSD.

chipset. Even if the information appears cryptic, it may match an option you'll find when you install FreeBSD or configure it after installation.

> **Caution** Some chips, such as many recent video card and motherboard chipsets, generate so much heat that they're covered with heat sinks, which obscure chipset identification markings. Do not attempt to remove such heat sinks because you may damage the chip, and even if you don't, you'll have a hard time re-attaching the heat sink so that it does its job.

If you can't find mention of a device in HARDWARE.TXT, that doesn't necessarily mean that it won't work. The device might be known by multiple names, and you simply haven't found the one by which it's listed in the file. Try doing a Usenet search using `http://groups.google.com` or a web search using your favorite search engine using FreeBSD and the name you've discovered. You could also try simply installing FreeBSD; the OS automatically detects many devices, so you may learn if it works quickly enough.

![](img/f34d37e3abe9f4517128e54f80ab2616_76_0.png)

Figure 2-2. Device chipsets are usually labeled for easy identification.

If the device doesn't work, you have three choices:

- **Replacement** You can replace the nonfunctional device with a supported model. This is often the most effective and simplest course of action, particularly with inexpensive devices such as Ethernet or sound cards. Many motherboard components, although they can't be removed, can be circumvented by adding a card that duplicates the motherboard component's function. You may need to disable the motherboard component in the computer's BIOS, though.
- **Workaround** It may be possible to work around an incompatibility in some way. In some cases, this may mean using a device in some sort of compatibility mode that provides limited functionality. For instance, some printers work with a lower resolution using a common protocol that FreeBSD (or, more precisely, Ghostscript) supports, while their higher-resolution modes remain inaccessible from FreeBSD. In other cases, you can do without the device entirely. For instance, you might not really need a sound card in FreeBSD, if you use the sound card mainly for games in Windows.
- **Driver development** If you have the programming skill or are willing to hire somebody with such skills, you can write a driver yourself or have it written for you. This task is well beyond the scope of this book, and it's useful mainly if you're a hobbyist programmer yourself or if the cost of replacing a component would be huge (for instance, replacing hundreds of expensive cards at a large site).

## Clearing Disk Space

FreeBSD needs disk space in which to operate. If you're installing FreeBSD to a new computer or replacing an existing OS, setting aside disk space requires no special preparation. As described in the upcoming section, "Partitioning the System," you can simply tell the installer to use all your disk space, and it will replace any existing data on the disk.

A more complex situation involves adding FreeBSD to an existing OS. In this case, you must set aside a dedicated primary partition for FreeBSD's use, as described in Chapter 1. Many FreeBSD CD-ROMS include an open source utility known as the First Non-Destructive Interactive Partition Splitting Program (`fips`; [http://www.igd.fhg.de/~aschaefer/fips/](http://www.igd.fhg.de/~aschaefer/fips/)). You can use this program to split an existing primary FAT partition into two parts. You can then use the FreeBSD installation program to delete the second partition and use its space. Another option is to use a third-party utility such as PowerQuest's ([http://www.powerquest.com](http://www.powerquest.com)) PartitionMagic. Such tools are often more flexible and easier to use than `fips`. One potentially very important advantage of PartitionMagic over `fips` is that PartitionMagic can shrink the New Technology File System (NTFS) partitions that are common with Windows NT, 2000, and XP installations. (Some of those systems use FAT, though, so don't assume `fips` is inadequate; check the filesystem type using the Windows Properties dialog box for the disk.)

> **Caution** FIPS, PartitionMagic, and other dynamic partitioning tools are inherently dangerous. Bugs, power outages, and other problems can cause data loss--potentially even destroying critical file system data structures, thus rendering access to all files on the disk impossible without difficult and potentially expensive repairs. For this reason, you should back up all your data before proceeding with such an operation.

## Using FIPS

To use FIPS to shrink an existing FAT partition, follow these steps:

1. In DOS or Windows, run a disk defragmenter on the c: partition. You can use the disk defragmentation options available from the Windows disk Properties dialog box, as shown in Figure 2-3. The idea is to ensure that all the files are in
