
yet. The RAM disk is essential if you are booting a SCSI disk and you haven't compiled the SCSI drivers into the kernel.

## ATA/ATAPI/MFM/RLL support

The next set of questions involves IDE devices, such as hard drives and ATAPI CD-ROM drives.

- ATA/ATAPI/MFM/RLL support

ATA/ATAPI/MFM/RLL support (IDE) [M/n/y/?]
Enhanced IDE/MFM/RLL disk/cdrom/tape/floppy support (BLK_DEV_IDE) [M/n/y/?]

When you're configuring an operating system, you have to expect a fair share of acronyms — this one has four acronyms: ATA, ATAPI, MFM, and RLL. All these relate to hard drives or the interface that links disk drives to the PC. Here's what they mean:

- ATA stands for AT Attachment and refers to the PC-AT style interface that connects hard drives and CD-ROM drives to the PC's motherboard.

- ATAPI stands for AT Attachment Packet Interface and refers to the original PC hard drives that integrate the disk controller onto the hard drive itself. This interface used to be called Integrated Drive Electronics, or IDE. You typically see the terms IDE, ATA, and ATAPI used interchangeably.

- MFM stands for Modified Frequency Modulation, which is the way data was encoded on older hard drives. These hard drives can work over an IDE interface.

- RLL stands for Run Length Limited, an old technique for storing data on a hard drive from the early days of the PC. RLL disks can work over an IDE interface.

The first question asks if you want the kernel to support IDE devices. The second question asks if you want to use the full-featured IDE device that can control up to ten IDE interfaces. Because each IDE interface can have a master and a slave device, this enables Linux to access a total of up to 20 IDE devices, such as disks or CD-ROM drives. You can press Enter to accept the default choices of module for both of these options.

The next set of options concerns various IDE drivers. You can accept the default answers for these options. Note that IDE/ATAPI FLOPPY refers to IDE floppy drives, such as the Iomega Zip drive or the IOMEGA Superdisk LS-120 drive. The questions about CMD640 and RZ1000 bug fixes refer to some known problems with specific chipsets used in IDE interfaces.

## SCSI device support

This set of options has to do with SCSI devices. SCSI stands for Small Computer Systems Interface — a type of interface through which you can connect multiple devices (such as hard drives and scanners) to the PC. If your system has a SCSI adapter, you should start by answering *Yes* to the *SCSI* option. After that, you have to answer questions about the types of devices (disk, tape, CD-ROM) connected to the SCSI adapter. Finally, you must enable support for the specific SCSI adapter model on your system.

## IEEE 1394 (FireWire) support

The next set of options is for enabling IEEE 1394 support, either as a module or linked into the kernel. IEEE 1394 is a high-speed serial bus for connecting peripherals to PCs. Apple calls this bus FireWire; Sony calls it iLink. IEEE 1394 is similar to USB, but it can transfer data at rates up to 400 Mbps, which is more than 30 times the data rate of the older USB version 1.1. (Note that USB 2.0 is much faster; it can transfer data at rates of up to 480 Mbps.) Because of its high data-transfer rates, IEEE 1394 is ideal for connecting high-speed peripherals, such as digital audio and video devices and external hard drives, to the PC.

Currently, Linux supports IEEE 1394 chipsets that are compatible with Texas Instruments PCI/lynx/PCILynx2 and OHCI chipsets. If your PC has an IEEE 1394 adapter, you can build the necessary drivers through these options.

- IEEE 1394 (*Firewire*) support
- IEEE 1394 (*Firewire*) support (*IEEE1394*) `[M/n/y/?]`

![](img/792720823146d68f19fd50c99ebfce4b_509_0.png)

To find out more about using IEEE 1394 peripherals in Linux, visit the Web site of the IEEE 1394 for Linux project at `www.linux1394.org`.

## I2O device support

Pronounced *eye-two-OH*, I2O refers to Intelligent Input/Output — a new device driver architecture independent of the operating system and the controlled device. I2O functions by logically separating the part responsible for managing the device from the part that contains operating system-specific details. (The logical separation of the driver’s capabilities is called the *I2O Split Driver model*.) The two parts of an I2O driver are the OS Services Module (OSM), which works with the operating system, and the Hardware Device Module (HDM) that interfaces with the particular device the driver manages. The OSM and HDM communicate by passing messages to each other.

Linux comes with some I2O drivers for SCSI and PCI devices. You can build the I2O drivers through the following configuration options:

I2O device support

- I2O support (I2O) [M/n/y/?]
- I2O Configuration support (I2O_CONFIG) [M/n/?]
- I2O Block OSM (I2O_BLOCK) [M/n/?]
- I2O SCSI OSM (I2O_SCSI) [M/n/?]
- I2O /proc support (I2O_PROC) [M/n/?]

## Networking support

This set of options deals with networking. How you set these options depends on how you want to use your Linux system in a network. Always say Yes to the TCP/IP Networking option because the X Window System uses TCP/IP networking (even if your PC isn’t on any network). You can also enable experimental support for IPv6 — the next-generation Internet Protocol.

Answer Yes to the Network packet filtering option if you want to use your Linux system as a *firewall* — an intermediary system that controls information flowing between a local area network (LAN) and the Internet.

Other categories in the Networking Support options include wireless LAN, Ethernet (10/100 Mbps as well as Gigabit), ATM (Asynchronous Transfer Mode), Token ring, ARCnet, AppleTalk, wide area network (WAN), PCMCIA network devices, amateur radio, infrared, and Bluetooth. For Ethernet, you can build support for the Ethernet card installed on your system. This category also includes support for wireless networking and drivers for wireless Ethernet cards. You can also enable experimental support for SCTP — Stream Control Transmission Protocol — designed to transport public switched telephone network signaling messages over IP networks (RFC 3758 describes SCTP).

The infrared support is for infrared communication using the protocols specified by the Infrared Data Association (IrDA). IrDA communication is used by many laptops and personal digital assistants (PDAs), such as Palm and Handspring. Many IR interfaces are in the form of *dongles* — small adapters that typically attach to the serial port of the PC. You can use the options in this section to enable support for several common types of dongles.

Bluetooth is a low-power, short-range wireless technology for connecting devices on the 2.4 GHz frequency band. Devices that use Bluetooth can usually connect when they are within 10 meters of one another. To find out more about Bluetooth, visit www.bluetooth.com. Linux supports Bluetooth through a core driver and several other modules. You can answer y to enable Bluetooth support and then select other options specific to your Bluetooth device.

### ISDN subsystem

This set of options enables you to include support for *ISDN* (Integrated Services Digital Network) — a digital telephone line that you can use to connect the Linux system to the Internet. These ISDN-related options include the configuration of specific ISDN adapters.

Build the ISDN driver only if your PC has an ISDN card. If you anticipate adding an ISDN card and purchase ISDN service from the phone company, you can build the driver as a module.

### Telephony support

With the right hardware and software, the Telephony Support options enable you to use the Linux system for making phone calls over the Internet (also known as *voice over Internet Protocol* or *VoIP*). You can choose to build driver modules for telephony support if you have a telephony card, such as the Internet PhoneJACK or Internet LineJACK manufactured by Quicknet Technologies, Inc. If you don’t have a telephony card, you can safely leave these options turned off.

### Input devices and character devices

The next few options deal with configuring input devices such as keyboard, mice, joystick, and touch screens, as well as devices connected to the serial and parallel ports. These options also include configuration of multiport serial interface cards that enable you to connect multiple terminals or other devices to your Linux system. Answer *No* if you do not have any such devices on your system. Near the end of the list, you see a question about parallel printer support (*PRINTER*). If you plan to connect a printer to the parallel port, answer *Yes* to this option.

### Watchdog timer

These configuration options enable you to turn on support for the watchdog timer. Essentially, this causes the kernel to create a special file; failure to open the file and write to it every minute causes the system to reboot. Some watchdog boards can monitor the PC’s status (including the temperature). You can also enable support for specific watchdog cards from this set of options.

If you want access to the PC’s nonvolatile (battery-backed) memory — *NVRAM* — in the real-time clock, answer *Yes* to the *NVRAM* option. You can access the real-time clock by enabling the *RTC* option.

### Floppy tape drive

If you have a tape drive connected to your floppy controller, answer *y* or *m* to the next option and select the other parameters appropriately (or accept the default choices):
