# Chapter 19 = Test Using Linux USB

You can find additional information on how to configure and test Linux USB Ethernet in http://www.linux-usb.org/usbnet/ and http://www.linux-usb.org/gadget/.

# HID (Human Interface Devices) USB Gadget

The USB-IF defines the requirements of USB HID devices and is available at http://www.usb.org/developers/hidpage/, which includes a mouse, keyboard, joystick, and more. On the latest Linux after 2.6.34, the HID gadget functional driver is implemented as part of http://lxr.free-electrons.com/source/drivers/usb/gadget/hid.c, and the host HID support is implemented through files in drivers/hid/usbhid. Figure 19.4 illustrates Linux USB HID modules in simple blocks.

The HID devices are represented as /dev/hidX, and you can read/write through that file. The Linux documentation in http://lxr.free-electrons.com/source/Documentation/usb/gadget_hid.txt includes a small interactive test program hid_gadget_test allows you to test HID setup. You can also read http://lxr.free-electrons.com/source/Documentation/usb/hiddev.txt to learn more using HID devices.

![](bbox=[0.085, 0.573, 0.691, 0.836])

Figure 19.4
Linux USB HID modules in simple blocks.