![](bbox=[0.14, 0.12, 0.25, 0.18])

Data transfer speeds may be expressed in bits per second (bps) or multiples thereof, such as megabits per second (Mbps) or gigabits per second (Gbps); or in bytes per second (B/s) or multiples thereof, such as megabytes per second (MB/s). In most cases, there are 8 bits per byte, so multiplying or dividing by eight may be necessary if you're trying to compare speeds of devices that use different measures.

USB is the preferred interface method for many external devices, including printers, scanners, mice, digital cameras, and music players. USB keyboards, Ethernet adapters, modems, speakers, hard drives, and other devices are also available, although USB has yet to dominate these areas as it has some others.

Most computers ship with four to eight USB ports. (A few years ago, two USB ports were more common.) Each port can handle one device by itself, but you can use a USB hub to connect several devices to each port. Thus, you can theoretically connect huge numbers of USB devices to a computer. In practice, you may run into speed problems, particularly if you're using USB 1.x for devices that tend to transfer a lot of data, such as scanners, printers, or hard drives.

![](bbox=[0.14, 0.47, 0.25, 0.55])

If you've got an older computer that only supports USB 1.x, and you want to connect a high-speed USB 2.0 or 3.0 device, buy a separate USB 2.0 or 3.0 board. You can use this board for the faster device and either disable the onboard USB 1.x ports or use them for slower devices.

# Linux USB Drivers

Several different USB controllers are available, with names such as UHCI, OHCI, EHCl, and R8A66597. Modern Linux distributions ship with the drivers for the common USB controllers enabled, so your USB port should be activated automatically when you boot the computer. The UHCI and OHCI controllers handle USB 1.x devices, but most other controllers can handle USB 2.0 devices. You need a 2.6.31 or later kernel to use USB 3.0 hardware. Note that these controllers merely provide a means to access the actual USB devices (mice, printers, and so on). Chances are you'll be most interested in the tools and utilities that enable you to use these devices.

You can learn a great deal about your devices by using the lsusb utility. A simple use of this program with no options reveals basic information about your USB devices:

```
$ lsusb
Bus 003 Device 008: ID 0686:400e Minolta Co., Ltd
Bus 003 Device 001: ID 0000:0000
Bus 002 Device 002: ID 046d:c401 Logitech, Inc. TrackMan Marble Wheel
Bus 002 Device 001: ID 0000:0000
Bus 001 Device 001: ID 0000:0000
```