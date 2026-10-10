![](bbox=[0.23, 0.07, 0.78, 0.55])

A USB-serial driver is similar to other USB client drivers except that it avails the services of a USB-Serial core in addition to the USB core. The USB-Serial core provides the following:

+   - A tty driver that insulates low-level USB-to-serial converter drivers from higher serial layers such as line disciplines.
+   - Generic probe() and disconnect() routines that individual USB-serial drivers can leverage.
+   - Device nodes to access USB-serial ports from user space. Applications operate on USB-serial ports via /dev/ttyUSBX, where X is the serial port number. Terminal emulators such as minicom and protocols such as PPP run unchanged over these interfaces.

A low-level USB-to-serial converter driver essentially does the following:

+   1. Registers a usb_serial_driver structure with the USB-Serial core using usb_serial_register(). The entry points supplied as part of usb_serial_driver form the crux of the driver.