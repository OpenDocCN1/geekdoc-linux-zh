# # FireWire

FireWire (aka IEEE-1394 or i.Link) is the latest external connection technology. FireWire resembles USB in many respects—it's a serial technology that enables adding or removing devices while the computer is powered up. It's much faster than USB, however—it runs at up to 50MB/s, compared to 1.5MB/s for USB, with faster versions under development. These characteristics make FireWire an appealing technology for use with external disk devices.

Unfortunately, in early 2000, FireWire is largely vaporware. A few FireWire devices exist, but they're quite rare. FireWire drivers have appeared in late 2.3.x series kernels, but these drivers aren't yet available for 2.2.x kernels. Check http://eclinux.uni-klu.ac.at/ieee1394 for more details.

# # PC-Card Interface

The PC-Card interface is used primarily by notebook computers to support assorted devices, including removable media drives. Some drives come with, or support as accessories, converters that let you use some other type of interface via a special PC-Card. Others let you plug a removable media device directly into the PC-Card slot.

Some notebook computers provide an option to use a *Zip* or LS-120 drive instead of a floppy disk or as a swap-out option in the same bay as a CD-ROM drive. These interfaces are likely to be faster than a PC-Card interface, and so are preferable in many cases to a PC-Card drive. Nonetheless, you might want to use a PC-Card interfaced drive for some reason, such as a greater ability to use the drive with other systems, such as a desktop computer.

# # Linux Compatibility with Removable Disks

Using removable disks with Linux is no more complex than is using a conventional fixed disk, although you do need to understand the rules for device files, mount options, and so on. Configuring your system to use a removable device sometimes poses challenges, however, because you must add appropriate devices drivers to the kernel, and it might not be obvious which drivers you need to add.

# # Kernel Options for Accessing Drives

When you configure your kernel for removable devices, you might need to check in several locations for appropriate device drivers. If you configure your Linux kernel by issuing the `make xconfig` command in the Linux source code directory (generally `/usr/src/linux`), you deal with two windows, which are shown in Figure 6.3. The first is the Linux Kernel Configuration window, which lists various broad classes of drivers and configuration options, such as *General setup* and *Block devices*. The second is the window you get when you click on any of these