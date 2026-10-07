# Chapter 16 = USB Virtual File Systems

From the output, you can infer that the thumb drive is assigned with device number 2 and is connected to port 3 of the USB with bus number 7. The output also shows you the drivers attached to the device. The script generates additional information, such as the product and vendor ID, when you invoke it with argument -1.

# usbfs: BBB/DDD Files

The next files are the BBB/DDD files of the usbfs, which control and interact with a USB device. This directory tree is created based on the USB number (BBB) and the USB device number (DDD). Unlike the devices file, the BBB/DDD file is in binary format. The following terminal activity shows you how the BBB/DDD files are organized in the /proc/bus/usb directory.

```
root@rajam-laptop:/proc/bus/usb# tree -A
++ 001
|-- 001
|-- 002
|-- 001
.
++ 003
|-- 001
|-- 004
|-- 001
|-- 005
|-- 001
|-- 006
|-- 001
|-- 002
|-- 007
|-- 001
|-- 002
|-- 003
-- devices
```

From the terminal log, you can infer that the thumb drive with device number 007. The contents of the file 002 is listed below the directory under bus number 007. The include device and configuration descriptors of the USB device. To interface with the device, open the device using the /proc/bus/usb/007/002 path. After a