
## Telephony Support

Telephony support is the product of work done by Quicknet Technologies (http://www.quicknet.net) to support their Internet PhoneIACK and Internet LineIACK telephone, key system, and PBX connectors for Voice over IP (VoIP) applications. These drivers are *highly* experimental and are only intended as development tools for Quicknet card owners.

## ATA/IDE Support

Linux will support up to eight low-cost ATA/IDE drives. With Linux 2.1/2.2, support was also added for IDE ATAPI floppy drives, tape drives, and CD-ROM drives (with auto-detection of interfaces), IRQs, and disk geometries. The new driver now adds support for PIO modes on OPTI chipsets, SCSI host adapter emulation, and PCI Bus-master DMA, as well as support for many PCI chipsets, and detection of buggy PCI IDE systems, such as the *perfect* feature of the RZ1000 or “IRQ unmasking” on the CMD640. Full details of the IDE driver and supported systems can be found in `linux/Documentation/ide.txt`.

While the driver automatically probes for disk drives, geometries, and IRQs, these interfaces may be specified using kernel bootparam. For example, to set the port addresses and the IRQ for the fourth controller set `ide3=0x168,0x366,10`.

The driver will probe for the IRQ if it is omitted. Any number of interfaces may also share an IRQ, although this will degrade performance. The driver will detect and account for this situation, but your controller cards may suffer damage in the process (theoretically).

Disk geometry can also be specified on the command line as three numbers for sectors, cylinders, and head, as in `hdc=768,16,32`. If your CD-ROM is not being detected, you can give the kernel an extra nudge by using the `hdd=cdrom` option.

IDE interfaces on sound cards may require initialization before they can be used. The program to initialize the driver is most often among the software that comes with the card and is usually part of the MS-DOS driver—the only alternative for using these devices is to boot your computer under MS-DOS, to allow the drivers to initialize the device, and then to use `loadlin` to switch to Linux.

Older hard drives may not be compatible with the newer IDE driver. In this situation, you can include both interfaces in the kernel. The older driver will command the primary IDE interface while still allowing newer hardware to be used on the other interfaces.

**Caution**

When passing IDE options to loadable modules using bootparams, substitute semicolons (;) for any commas in the command line, for example:

```
insmod ide.o options="ide0=serialize ide2=0x1e0;0x3ee;11"
```

## SCSI Support

SCSI drives are more expensive than IDE, but give much higher performance and are the method of choice for large enterprise servers. Linux SCSI support is also required for certain parallel-port disk devices, such as the Omeqa ZIP drive. Linux also supports SCSI CD-writers, scanners, and synthesizers via the SCSI Generic option, and provides options for logging errors and activity on these devices.

To enable SCSI support, you need to know your hardware. The Low-Level Drivers dialog presents a long list of supported adapters, with some options for setting device parameters.

## IEEE 1394 FireWire Support

FireWire is a high-performance serial bus, also known as i.Link and described by the IEEE 1394 standard. This hardware is most often used with digital video cameras and other high-speed peripherals, and I/O cards with this support are available from Texas Instruments, Adaptec, and on the Miro DV boards. With the exception of the RAW option to enable direct manipulation of FireWire by userspace programs, the remaining options in this section select among specific vendor implementations.

## I²O Support

Intelligent Input/Output uses a coprocessor for interface adapters and is designed to separate the logical device from the physical implementation. Drivers for I²O devices can be written to an abstract Operating System Module (OSM) definition that is portable across many hardware implementations of the standard. These devices include block devices (disks), network interfaces, and SCSI devices.

I²O also includes a sysctl option to allow probing the driver through the /proc/i2o files.

## Network Device Support

If you have a network card, you must specify the network hardware. If you have a network card but don't know what it is, if it is a cheap one, it is more than likely an NE2000-compatible.

The main network device option links in the basic network subsystem. You must enable this support even if you only connect to networks via local SLIP, PPP, or PLIP, or if your machine will dial an ISP to connect to the Internet.

## Dummy Network Device

The Dummy device is just that: It holds a place for a device and discards any traffic sent to it. This is most often used to make **SLIP** or **PPP** interfaces appear to be active even while offline. For example, if you are using a demand-dialing program such as `diald`, the Dummy device will enable network programs to function, but the packets sent to this interface will be re-routed through to the Internet after the dialer has established the connection.

## EQL and Ethernet Bonding

**EQL** is rarely used, but extremely useful. In these days of wave modems and cheap xDSL lines, we often forget that many do not have the luxury of cheap, high-speed dialup lines. Using EQL, Linux can bind together several modems as the same IP interface and effectively multiply the bandwidth. For example, a rural school could install a Linux gateway server with demand-dialing sensitive to the bandwidth requirements. When one phone line became saturated (old-corrode rural lines are often 31.2KB), a second line could be opened to the same ISP, and then a third, and so on, giving the school symmetric, ISDN-like bandwidth for the cost of a few extra phone lines. EQL does require support at both ends of the connection. It works very well with the Livingstone Portmaster 2e, which is fortunately a popular choice among smaller ISPs.

> **Note**
> Unfortunately, EQL requires support at the remote end and this often prevents its use in remote areas. Eqplus (<http://www.cwarreo.com/eqpl.us.html>) is a Linux modem combining strategy based upon IP masquerading and eql. This package includes kernel patches to the EQL support to allow multiple connections to any external networks.

Ethernet Bonding provides the same service for ethernet cards, tying together multiple network interfaces as a single virtual interface.

## PLIP, PPP, and SLIP Dialup Networking Support

PLIP is a means to network two machines over a null-printer (“Turbo Laplink”) cable to provide four or eight parallel data channels. This is often used to NFS-install to a laptop where there is no CD-ROM. Wiring for this cable is described in `Documentation/networking/PLIP.txt`. Russell Nelson has also created MS-DOS drivers for PLIP to connect DOS-based machines (such as that old PS/1 space heater I keep in the workshop).

SLIP is the ancestor of PPP, and although 99.9% of all ISPs will only offer PPP connections, SLIP still has some viable uses. SLIP is an essential ingredient as an intermediary device in the diald demand dialer or to gain a network connection over a telnet session (using SLIRP).

## Amateur Radio and Wireless Support

Another low-cost Internet solution for impossible remote locations is the Amateur Radio Support. By encoding packets over short-wave radio, Linux systems have been used to provide as much as 64Kb of symmetric bandwidth over long distances. For examples of packet radio in action, see the Wireless Papers (http://www.ictp.trieste.it/~radionet/papers) or visit the Packet Radio home page (http://www.tapr.org/tapr/html/pkthome.html).

A related feature of interest to campus and rural development projects is the kernel support for Wireless LAN, AT&T WaveLAN, and DEC RoamAbout DS (see Documentation/networking/wavelan.txt). There is also support for the MosquitoNet (http://mosquitonet.stanford.edu) StarMode RadioIP systems used by many laptop owners.

## IrDA: Infrared Port Device Drivers

Infrared Data Associations protocols provide wireless infrared communications between laptops and PDAs at speeds up to 4Mbps, and the Linux driver makes supported devices transparent to the networking system. More information on this support, and on the utility programs for IrDA, can be found at the Linux Documentation Project (http://www.linuxdocs.org) or the Linux IrDA home page (http://www.cs.uiz.no/linux-irda/).

## ISDN Subsystem

To use ISDN, you must obtain the isdn4k-utils utility programs (ftp://ftp.franken.de/pub/isdn4linux). When the module is loaded, isdn.o can support up to 64 channels (you can add more by changing the isdn.h file directly). Each channel will be given read/write access to the D-Channel messages and iocli functions, with non-synchronized read/write to B-Channel and I28 tty-devices. Modem emulation provides a standard AT-style command set compatible with most dialup tools, such as minicom, pppd, and mgetty.

The second step in configuring for ISDN is to select your specific ISDN modem card. Some ISDN cards will require initialization before the vendor-independent setup. Details can be found in the appropriate README file under linux/Documentation/isdn.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_912_0.png)
