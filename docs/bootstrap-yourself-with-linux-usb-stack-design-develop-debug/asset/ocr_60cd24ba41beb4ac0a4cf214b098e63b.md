# Chapter 18 = Debugging Using Linux USB

[ 3907.638946) usb 7-3: control read: data 04 03 09 04
[ 3907.638961) usb 7-3: usbdev_ioctl: CONTROL
[ 3907.638968) usb 7-3: control read: bRequest=06 bRequestType=80 wValue=0301
Index=0409 length=0ff
[ 3907.639200) usb 7-3: control read: data 0c 03 55 00 64 00 69 73 00 6b 00 00 00 00
00 00
[ 3907.639229) usb 7-3: usbdev_ioctl: CONTROL
[ 3907.639235) usb 7-3: control read: bRequest=06 bRequestType=80 wValue=0300
Index=0000 length=0ff
[ 3907.639445) usb 7-3: control read: data 04 03 09 04

In the preceding log, you can see IOCTL transactions when the lsusb utility is executed. The log contains details on the time of UR activity, bus and device number, and USB transfer information. The log is not comprehensive as the usbmon, and debug data is captured at an initial stage of the URB.

# VERBOSE DEBUGGING FOR HOST-SIDE USB

The verbose debugging method is not specific to the USB subsystem, but it's a more traditional approach that kernel developers use for debugging. In this method, the debug message is controlled by a DEBUG macro, and the modules print debug messages only in the debug mode. In release mode, this macro is disabled, the debug messages are not printed. The USB subsystem verbose message is one such option available on Linux for debugging the USB subsystem. You can configure the verbose debug message through kernel configuration macros. Figure 18.10 illustrates how to enable the verbose debug option. The USB Debug Messages option mainly generates debug messages interleaved in the USB core and hub drivers' source of the Linux subsystem.

Sometimes it is necessary to generate debug information during the initial enumeration process by the usbcore to isolate problems, because neither usbmon nor usbfs_snoop covers this. For example, the initial USB device setup is done via the hub layer of the usbcore, which needs some more informative debug messages to isolate low-level error. To get additional debug messages, enable CONFIG_USB_ANNOUNCE_NEW_DEVICES in the hub.c through kernel configuration, as shown in Figure 18.10. This announces any new devices connected to the Linux USB subsystem. Sometimes such debug information helps you check whether the issue is in USB enumeration or lower in the usbcore.