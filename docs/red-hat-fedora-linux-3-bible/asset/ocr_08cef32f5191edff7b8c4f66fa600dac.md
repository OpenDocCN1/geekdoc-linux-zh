> **NOTE:** FireWire is currently disabled in Fedora Core 3. This is due to some bugs that could cause Fedora installation to fail on a computer where a FireWire device is connected. There have been some indications that a fix might be available soon, so if FireWire devices are important to you, look for Fedora kernel updates in the near future.

# Supporting USB devices

The 2.6 kernel is a must for computer hardware that includes USB 2.0 devices. While some support for USB 2.0 devices has been backported to the 2.4 kernel, you can expect more solid support in the 2.6 kernel. USB 1.1 offered speeds of 1.5Mbps (low speed) and 12Mbps (full speed). Alternatively, USB 2.0 devices operating at their full potential (high speed) run at 480Mbps. This makes them appropriate for:

+   - High-quality Webcams
+   - Ethernet adapters running at 100BaseT
+   - External disk drives, used to provide portable storage in many applications, such as playing music, video, or other types of content

There have been compatibility problems with some USB 2.0 devices. Devices that are certified as USB 2.0 that will work with the Linux 2.6 kernel should display the red, white, and blue “Certified Hi-Speed USB” logo.

For the 2.6 kernel, there are generic USB drivers to handle sound (audio.ko), modems and ISDN adapters (cdc-acm.ko), printers (usblp.ko), and MIDI devices (usb-midi.ko). There are specific drivers to support Bluetooth devices, scanners, tablets, touch screens, digital cameras, FM radio devices, serial port boards, and mass storage devices.

For further information about USB 2.0 devices, that are supported in the 2.6 Linux kernel, refer to the Linux USB site (http://linux-usb.org).

# Running older hardware

Support for legacy hardware that has not been in previous Linux kernels has been added to the 2.6 Linux kernel. For example, plug-and-play extensions for Industry Standard Architecture (ISA) busses are included in the 2.6 kernel. Although MCA and EISA busses have been included in earlier Linux kernels, support for those architectures has been added to the new 2.6 kernel device database, also helping those architectures to support full plug-and-play extensions. In other words, more legacy hardware should be detected, configured, and managed automatically in the 2.6 kernel.

# Using the 2.6 Kernel Beyond Fedora Core

Although the first Linux kernel was created so that Linux Torvalds could have his home PC work like the UNIX operating systems he used at school, the latest 2.6 Linux kernel can stretch well outside the boundaries of the average PC.