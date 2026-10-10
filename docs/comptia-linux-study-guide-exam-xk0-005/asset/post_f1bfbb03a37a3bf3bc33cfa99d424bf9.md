
The USB standard has evolved over the years. The original version 1.0 only supported data transfer speeds up to 12 Mbps. The 2.0 standard increased the data transfer speed to 480 Mbps. The current USB standard, 4.0, allows for data transfer speeds up to 40 Gbps, making it useful for high-speed connections to external storage devices.

A myriad of devices can connect to systems using the USB interface. You can find hard drives, printers, digital cameras and camcorders, keyboards, mice, and network cards that have versions that connect using the USB interface.

## Linux and USB devices

There are two steps to get Linux to interact with USB devices. The first step is that the Linux kernel must have the proper module installed to recognize the USB controller installed on your server, workstation, or laptops. The controller provides communication between the Linux kernel and the USB bus on the system. When the Linux kernel can communicate with the USB bus, any device you plug into a USB port on the system will be recognized by the kernel but is not necessarily usable. The second step is that the Linux system must have a kernel module installed for the individual device type plugged into the USB bus. Linux distributions have a wide assortment of modules installed by default. Should you run into a USB device that doesn't work on your Linux system, refer to Chapter 14 for information on installing kernel modules.

## The GPIO Interface

The general-purpose input/output (GPIO) interface has become popular with small utility Linux systems designed for controlling external devices for automation projects. This includes popular hobbyist Linux systems such as the Raspberry Pi and BeagleBone kits.

The GPIO interface provides multiple digital input and output lines that you can control individually, down to the single-bit level. The GPIO function is normally handled by a specialty integrated circuit (IC) chip, which is mapped into memory on the Linux system.

The GPIO interface is ideal for supporting communications to external devices such as relays, lights, sensors, and motors. Applications can read individual GPIO lines to determine the status of switches, turn relays on or off, or read digital values returned from any type of analog-to-digital sensors such as temperature or pressure sensors.

With the GPIO interface, you have a wealth of possibilities for using Linux to control objects and environments. You can write programs that control the temperature in a room, sense when doors or windows are opened or closed, sense motion in a room, or even control the operation of a robot.

## The /dev Directory

Once the Linux kernel can communicate with a device on an interface, it must be able to transfer data to and from the device. For many devices, this is done using device files. Device files are files that the Linux kernel creates in the special /dev directory to interface with hardware devices.

To retrieve data from a specific device, a program just needs to read the Linux device file associated with that device. The Linux operating system handles all the intricacies of interfacing with the actual hardware. Likewise, to send data to the device, the program just needs to write to the Linux device file.

As you add hardware devices such as USB drives, network cards, or hard drives to your system, Linux creates a file in the /dev directory representing that hardware device. Application programs can then interact directly with that file to store and retrieve data on the device. This is much easier than requiring each application to know how to directly interact with a device.

There are two types of device files in Linux, based on how Linux transfers data to the device:

-   Character device files: Transfer data one character at a time. This method is often used for serial devices such as terminals and USB devices.
-   Block device files: Transfer large blocks of data. This method is often used for high-speed data transfer devices such as hard drives and network cards.

The type of device file is denoted by the first letter in the permissions list, as shown in Listing 23.1.

### Listing 23.1: Partial output from the /dev directory

```bash
$ ls -al sd* tty*
brw-rw---- 1 root disk  8, 0 Feb 16 17:49 sda
brw-rw---- 1 root disk  8, 1 Feb 16 17:49 sda1
crw-rw-rw- 1 root tty   5, 0 Feb 16 17:49 tty
crw-w----- 1 root tty   4, 0 Feb 16 17:49 tty0
crw-w----- 1 gdm  tty   4, 1 Feb 16 17:49 tty1
```

The hard drive devices, sda and sda1, show the letter b, indicating that they are block device files. The tty terminal files show the letter c, indicating that they are character device files.

There are also a few special character device files that provide useful features for the shell. Ones of note are as follows:

-   /dev/null: When data is redirected to this device, the data is discarded. This is handy for redirecting program messages that you don’t want displayed.
-   /dev/random and /dev/urandom: These device files provide access to the kernel’s random number generator. The /dev/random device blocks requests until enough random data has been generated to calculate a true random number.
-   The /dev/urandom device doesn't block but just returns a random number using the random data currently available. Though less accurate, it's usually fine for most random number uses.
-   /dev/zero: When data is read from this device, it returns a NULL character (0x00). This is an excellent resource for creating null files, or erasing previously stored data on a disk partition.

Besides device files, Linux also provides a system called the *device mapper*. The device mapper function is performed by the Linux kernel. It maps physical block devices to virtual block devices. These virtual block devices allow the system to intercept the data written to or read from the physical device and perform some type of operation on them. Mapped devices are used by the Logical Volume Manager (LVM) for creating logical drives and by the Linux Unified Key Setup (LUKS) for encrypting data on hard drives.

![](img/c0a399aca0d18f8822d714ad0a173123_713_0.png)

## The /proc Directory

The `/proc` directory is one of the most important tools you can use when troubleshooting hardware issues on a Linux system. It's not a physical directory on the filesystem but instead a virtual directory that the kernel dynamically populates to provide access to information about the system hardware settings and status.

The Linux kernel changes the files and data in the `/proc` directory as it monitors the status of hardware on the system. To view the status of the hardware devices and settings, you just need to read the contents of the virtual files using standard Linux text commands.

There are different `/proc` files available for different system features, including the IRQs, I/O ports, and DMA channels in use on the system by hardware devices. The following sections discuss the files used to monitor these features and how you can access them.

### Interrupt Requests

Interrupt requests (called IRQs) allow hardware devices to indicate when they have data to send to the CPU. The PnP system must assign each hardware device installed on the system a unique IRQ address. You can view the current IRQs in use on your Linux system by looking at the `/proc/interrupts` file using the Linux `cat` command, as shown in Listing 23.2.

#### Listing 23.2: Listing system interrupts from the /proc directory

```bash
$ cat /proc/interrupts
               CPU0
0:         36  IO-APIC  2-edge     timer
1:        297  IO-APIC  1-edge    i8042
8:      0 IO-APIC  8-edge      rtc0
9:      0 IO-APIC  9-fasteoi   acpi
12:     396 IO-APIC 12-edge     i8042
14:      0 IO-APIC 14-edge     ata_piix
15:     914 IO-APIC 15-edge     ata_piix
18:      2 IO-APIC 18-fasteoi  vboxvideo
19:    4337 IO-APIC 19-fasteoi  enp0s3
...
```

In Listing 23.2, the first column indicates the IRQ assigned to the device. Some IRQs are reserved by the system for specific hardware devices, such as 0 for the system timer and 1 for the system keyboard. Other IRQs are assigned by the system as devices are detected at boot time.

### I/O Ports

The system I/O ports are locations in memory where the CPU can send data to and receive data from the hardware device. As with IRQs, the system must assign each device a unique I/O port. This is yet another feature handled by the PnP system.

You can monitor the I/O ports assigned to the hardware devices on your system by looking at the /proc/ioports file, as shown in Listing 23.3.

#### Listing 23.3: Displaying the I/O ports on a system

```bash
$ cat /proc/ioports
0000-0cf7 : PCI Bus 0000:00
0000-001f : dma1
0020-0021 : pic1
0040-0043 : timer0
0050-0053 : timer1
0060-0060 : keyboard
0064-0064 : keyboard
0070-0071 : rtc_cmos
0070-0071 : rtc0
0080-008f : dma page reg
00a0-00af : pic2
00c0-00df : dma2
00f0-00ff : fpu
0170-0177 : 0000:00:01.1
0170-0177 : ata_piix
01f0-01f7 : 0000:00:01.1
01f0-01f7 : ata_piix
```
