
## 504 Rebuilding the Kernel

![](img/9f89727199836b0f871f1745838aa8b2_530_0.png)

If you scroll down the list of options in the upper-right pane in Figure 6-3, you find more options for block devices. Turning on the Loopback Device Support option lets the Linux kernel manipulate an entire file system image stored in a single large file. This option is useful if you want to mount a CD image (for example, a Fedora Core ISO file) and check it out before actually burning the CD.

The RAM Disk Support option allows the kernel to use a portion of your system's memory as a disk capable of storing a file system. The initial RAM Disk Support option creates a RAM disk that is used by the boot loader before the system boots. The initial RAM disk functions only during system startup when the hard drive may not be available yet. The initial RAM disk is essential for loading the driver modules needed to access the hard disk before the kernel can boot from a hard drive partition.

### ATA/ATAPI/MFM/RLL support

When you're configuring an operating system, you have to expect a fair share of acronyms — this one has four acronyms: ATA, ATAPI, MFM, and RLL. All these relate to hard drives or the interface that links disk drives to the PC. Here's what they mean:

- **ATA** stands for *AT Attachment* and refers to the PC-AT style interface that connects hard drives and CD-ROM drives to the PC's motherboard.
- **ATAPI** stands for *AT Attachment Packet Interface* and refers to the original PC hard drives that integrate the disk controller onto the hard drive itself. This interface used to be called *Integrated Drive Electronics* or IDE. You typically see the terms IDE, ATA, and ATAPI used interchangeably.
- **MFM** stands for *Modified Frequency Modulation*, the way data was encoded on older hard drives. These hard drives can work over an IDE interface.
- **RLL** stands for *Run Length Limited*, an old technique for storing data on a hard drive from the early days of the PC. RLL disks can work over an IDE interface.

Enable the **ATA/ATAPI/MFM/RLL Support** option by clicking it until a checkmark appears. When you enable this support, you get many more configuration options (see Figure 6-4) involving IDE devices, such as hard drives and ATAPI CD-ROM drives.

The first option is for **enhanced IDE support**, which refers to full-featured IDE controllers that can control up to 10 IDE interfaces. Because each IDE interface can have a master and a slave device, Linux can access a total of up to 20 IDE devices (such as disks or CD-ROM drives). Make sure this option has a check mark.

![](img/9f89727199836b0f871f1745838aa8b2_531_0.png)

![](img/9f89727199836b0f871f1745838aa8b2_532_0.png)

The second item in the upper-right pane of Figure 6-4 is a comment that refers you to the file Documentation/ide.txt for help with IDE devices. To read these help files (these are all text files), type the following command to change the directory:

```
cd /usr/src/linux*/Documentation
```

Now you can browse the directory for text files relating to specific devices. You can also use the GNOME or KDE file managers to browse the documentation.

> Note: The IDE/ATAPI FLOPPY Support option refers to IDE floppy drives, such as the Iomega Zip drive or Imation SuperDisk LS-120 drive. If you have an IDE ZIP drive, enable this option to show a check mark or a dot.

### SCSI device support

SCSI stands for Small Computer Systems Interface — a type of interface through which you can connect multiple devices (such as hard drives and scanners) to the PC. This set of options has to do with SCSI devices. If your system has a SCSI adapter, start by clicking the SCSI Support option to show a dot (which means a module is built). After that, you can set the options relating to the types of devices (disk, tape, CD-ROM) connected to the SCSI adapter. Finally, you must look in the SCSI low-level drivers category and enable support for the specific SCSI adapter model on your system.

### IEEE 1394 (FireWire) support

IEEE 1394 is a high-speed serial bus for connecting peripherals to PCs. Apple calls this bus FireWire; Sony calls it i.LINK. IEEE 1394 is similar to USB, but it can transfer data at rates up to 400Mbps, which is more than 30 times the data rate of the older USB version 1.1 (note that USB 2.0 is even faster; it can transfer data at rates of up to 480Mbps). Because of its high data-transfer rates, IEEE 1394 is ideal for connecting high-speed peripherals such as digital audio and video devices and external hard drives to the PC.

You can build a module for the IEEE 1394 bus. Currently, Linux supports IEEE 1394 chipsets that are compatible with Texas Instruments PCILynx/PCILynx2 and OHCI chipsets. If your PC has an IEEE 1394 adapter, you can build the necessary drivers through these options.

![](img/9f89727199836b0f871f1745838aa8b2_532_1.png)

To find out more about using IEEE 1394 peripherals in Linux, visit the Web site of the IEEE 1394 for Linux project at www.linux1394.org.

### I2O device support

Pronounced *eye-two-oh*, I2O refers to Intelligent Input/Output — a new device driver architecture independent of the operating system and the controlled device. The basic concept of I2O is to separate the part responsible for managing the device from the part that contains operating system-specific details (it's called the I2O Split Driver model). The two parts of an I2O driver are the OS Services Module (OSM), which works with the operating system, and the Hardware Device Module (HDM) that interfaces with the particular device the driver manages. The OSM and HDM communicate by passing messages to each other. Linux comes with some I2O drivers for SCSI and PCI devices. You can configure these drivers from this category of options.

### Networking support

This set of options (shown in Figure 6-5) deals with networking. How you set these options depends on how you want to use your Fedora Core system in a network. Always enable the TCP/IP Networking option because the X Window System uses TCP/IP networking (even if your PC isn't on any network).

![](img/9f89727199836b0f871f1745838aa8b2_533_0.png)

**Figure 6-5:** Configure the networking options from this category of options.

Set the Network Packet Filtering option to a check mark if you want to use your Fedora Core system as a firewall—an intermediary system that controls information flowing between a local area network (LAN) and the Internet.

Other categories in the Networking Support options include wireless LAN, Token Ring, wide area network (WAN), PCMCIA network devices, amateur radio, infrared, and Bluetooth.

The infrared support is for infrared communication using the protocols specified by the Infrared Data Association (IrDA). IrDA communication is used by many laptops and personal digital assistants (PDAs), such as Palm and Handspring.

Bluetooth is a low-power, short-range wireless technology for connecting devices on the 2.4 GHz frequency band. Devices that use Bluetooth can usually connect when they are within 10 meters of one another. To find out more about Bluetooth, visit www.bluetooth.com. Linux supports Bluetooth through a core driver and several other modules. You can click the option to enable Bluetooth support and then select other options specific to your Bluetooth devices.

### ISDN subsystem

This set of options enables you to include support for ISDN (Integrated Services Digital Network)—a digital telephone line you can use to connect the Linux system to the Internet. These ISDN-related options include the configuration of specific ISDN adapters.

Build the ISDN driver only if your PC has an ISDN card. If you anticipate adding an ISDN card and purchase ISDN service from the phone company, you can build the driver as a module. Read the file /usr/src/linux-*/Documentation/isdn/README for more information on how to set up and use the ISDN driver in Linux.

### Telephony support

With the right hardware and software, the Telephony Support options enable you to use the Fedora Core system for making phone calls over the Internet (also known as voiceover IP or VoIP). You can choose to build driver modules for telephony support if you have a telephony card, such as the Internet PhoneJACK or Internet LineJACK manufactured by Quicknet Technologies, Inc. If you have no Quicknet telephony cards, you can safely leave these options turned off.

### Character devices

These options deal with configuring character devices, which include devices connected to the serial and parallel ports. These options also
