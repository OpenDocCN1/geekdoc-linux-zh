hopefully find answers to how to make the hardware work with Linux. This is also a good way to research answers to questions about software issues.

# Preparing for Potential Hardware Problems

Fedora will work out-of-the-box with nearly every Intel- or PowerPC-based motherboard and laptop; drivers for thousands of different types of hardware peripherals are included. But you can sometimes run into problems if Linux does not recognize a hardware item, if Fedora does not correctly initialize the hardware, or if an initialized item is incorrectly configured. For these reasons, some hardware items are prone to creating problems during an install. In the sections that follow, you learn some important pointers for avoiding these problems or resolving those that do occur.

# Controllerless Modems

As you read earlier, most Linux hardware-related installation problems stem from a lack of technical specifications from the manufacturer, thwarting efforts of open source developers to create a driver. In the recent past, one hardware item that triggered both types of difficulties was the controllerless modem, also colloquially known as a WinModem. The good news is that modem chipset manufacturers have been more forthcoming with driver details. Some original equipment manufacturers, such as IBM, have made a concerted effort to provide Linux support. Support for the ACP Mwave modem, used in ThinkPad 600/Es and 770s, is included in the Linux kernel. Drivers have been developed for many of the controllerless modem chipsets that formally did not work with Linux.

If a driver is not available for your controllerless modem, you have a few options. You can download the driver's source code and build the driver yourself. Alternatively, you can download a binary-only software package and install the driver.

Some controllerless modems might also need to be initialized and configured using a separate utility program. The modem, if supported, should work normally after installing and configuring the driver.

You can research Linux support for controllerless modems by browsing to http://www.linmodems.org/.

# Universal Serial Bus Devices

Fedora supports hundreds of different Universal Serial Bus (USB) devices. USB is a design specification and a protocol used to enable a host computer to talk to attached peripherals. Because of lack of manufacturer and device ID information or lack of technical specifications regarding certain chipsets, some devices might not work with Fedora. USB 1.1 devices are designed to support data transfer speeds between 1.5 and 12Mbps.

Common USB devices include cameras, keyboards, mice, modems, network interfaces, printers, scanners, storage devices, video (such as webcams), and hubs (to chain additional devices). Some problematic USB devices (at the time of this writing) include

+   * **Wireless**—Many 802.11b/g wireless USB network adapters, with the exception of those using Atmel chipsets