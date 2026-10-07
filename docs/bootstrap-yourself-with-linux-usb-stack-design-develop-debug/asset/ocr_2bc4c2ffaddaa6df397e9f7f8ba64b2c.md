# Table 17.4 Miscellaneous Operations

| Operation | Description |
|---|---|
| usb_get_driver_np | Linux associates a driver for each interface of the USB device. This is informative at the user level to verify whether the driver is loaded for a particular interface. usb_get_driver_np returns the name of the driver associated with a particular interface. Internally, uses IOCTL_USB_GETDRIVER to retrieve the application's requirement from the usbcore module of the Linux USB host framework. |
| usb_detach_kernel_driver_np | Sometimes a requirement to detach a kernel driver from the interface. Internally, it uses IOCTL_USB_DISCONNECT to pass on the application's requirement from the usbcore module of the Linux USB host framework. |

utility is part of the usbtils package that was developed based on libusb. This section provides a brief overview of these applications and explores how to install and use them.

# libptp

PTP is a standard developed by camera vendors to provide a way of interfacing an imaging device and a PC. PTP specification suggests USB as its transport layer, which may consist of the most digital devices such as cameras use. The libptp functional driver connects USB-based PTP devices with a PC. The libptp extends libusb interfaces to detect and interact with PTP devices. Linux-based applications such as gphoto use libusb for image transfer. As a developer, you can also write test applications on this library and test PTP devices. The development effort of test tools for devices decreases significantly when you use such prevailed systems. You can download the source package from http://libptp.sourceforge.net/. You need to install libusb before you extract, build, and install the source in your machine.

# usbtils

As seen earlier, libusb is the most common command-line USB utility among USB developers. The tool reads device information, such as the descriptors, through libusb and displays it to the user in a more readable form. You can install libusb from its source package download from sourceforge.net/projects/linux-usb/, or you can use package installers as in Ubuntu apt-get install usbtils. You need to ensure that the system contains libusb for libusb to work.