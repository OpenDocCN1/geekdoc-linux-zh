# 510 Rebuilding the Kernel

# USB support

Use this category of options (see Figure 6-6) to configure support for the Universal Serial Bus (USB) — a bus that comes into most modern PCs. USB version 1.1 supports data-transfer rates as high as 12Mbps — 12 million bits per second or 1.5 Mbps per second — compared with 115Kbps or the 0.115Mbps transfer rate of a standard serial port (such as COM1). You can daisy chain up to 12 devices on a bus. The bus also provides power to the devices, and you can attach or remove devices while the PC is running — a commonly referred to as hot swapping or hotplug, USB version 2.0 (or USB 2, or USB2 for short) ups the data-transfer rate up to 480Mbps, slightly faster than the comparing IEEE 1394 (FireWire).

![](bbox=[0.265, 0.335, 0.803, 0.638])

Figure 6-6 Configure USB support through these options.

USB can replace the functionality of the PC's serial and parallel ports, as well as the keyboard and mouse ports. Nowadays, many peripherals — such as keyboard, printer, scanner, modem, digital camera, and so on — are designed to connect to the PC through a USB port.

If your PC has a USB Port, set the Support port option to a dot (so that a module is built). Then you have to select the UHCI or OHCI option, depending on the type of USB interface — UHCI (Intel) or OHCI (Compa and others) — your PC. To determine the type of USB interface, lspci in a terminal