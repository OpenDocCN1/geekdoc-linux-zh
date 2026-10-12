# USB support

Use this category of options (Figure 6-15) to configure support for the Universal Serial Bus (USB) — a serial bus that comes built into most new PCs. USB version 1.1 supports data-transfer rates as high as 12Mbps — 12 million bits per second or 1.5 megabytes per second — compared with 115Kbps or the 0.115Mbps transfer rate of a standard serial port (such as COM1). You can daisy-chain up to 127 devices on a USB bus. The bus also provides power to the devices, and you can attach or remove devices while the PC is running — a capability commonly referred to as hot swapping. USB version 2.0 (or USB 2.0 or USB2, for short) ups the data-transfer ante to 480Mbps, slightly faster than the competing IEEE 1394 (FireWire) bus.

![](bbox=[0.27, 0.42, 0.78, 0.78])

Figure 6-15
Configure USB support through these options.

USB can replace the functionality of the PC's serial and parallel ports, as well as the keyboard and mouse ports. Nowadays, many PC peripherals — such as mouse, keyboard, printer, scanner, modem, digital camera, and so on — are designed to connect to the PC through a USB port.

If your PC has a USB Port, set the USB support option to y or m. Then you have to answer m to the UHCI or OHCI option, depending on the type of USB interface — UHCI (Intel) or OHCI (Compaq and others) — your PC has. To determine the type of USB interface, type lspci and look for the USB controller's make and model in the output. If the controller is by Intel, use the UHCI driver.

For USB 2.0 support, you can set the EHCI HCD (that's host controller device) option to y or m.