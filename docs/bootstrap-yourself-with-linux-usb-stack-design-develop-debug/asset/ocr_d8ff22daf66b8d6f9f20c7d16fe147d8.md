# USB Monitor: usbmon 267

either use lsusb or see a devices exported by usbfs, generally in /proc/bus/ usb /devices. In the sample setup, the device with ID 1221:3234 is the device of interest, and lsusb lists the device lists along with the bus number.

```
root@rajar-laptop:~# lsusb
Bus 007 Device 003: ID 1221:3234
Bus 007 Device 001: ID 0000:0000
Bus 006 Device 002: ID 064e:a103
Bus 006 Device 001: ID 0000:0000
Bus 005 Device 001: ID 0000:0000
Bus 004 Device 001: ID 0000:0000
Bus 003 Device 001: ID 0000:0000
Bus 002 Device 001: ID 0000:0000
Bus 001 Device 001: ID 0000:0000
```

The device connected for this example is a mass storage device that is connected to the USB bus with bus 7. To capture the USB transactions of the mass storage device, you can write a simple application that can read and display the information to you, or you can use the cat command on the file representing the device and pipe it to a log file. In the following terminal activity, the device of interest is connected to bus 7 and piped to usbmclog.txt.

```
root@rajar-laptop:/sys/kernel/debug/usb#
root@rajar-laptop:/sys/kernel/debug/usb# cat 7u >usbmclog.txt
root@rajar-laptop:/sys/kernel/debug/usb#
```

You can analyze at your own pace the URB information captured in usbmclog.txt. The CD accompanying this contains the complete log file. For ease of analysis, you see only part of the log file that captured transaction of the mass storage device. The snippet contains a couple of control and bulk transactions that occurred between the Linux host and USB mass storage device.

If you look at the log illustrated next, you can interpret the first line of the log file as a CONTROL transfer in bus 7 targeting endpoint address 0. The control transfer is to the host with the USB address of 5 to the device. The second line capture the SET_ADDRESS URB completion process indicated by C with successful completion status 0.

```
d2263a80 261300221 S C:7:0000:0 05 00 0500 0000 0000 0
d2263a80 2613001276 C:7:0000:0 0 0
d2263a80 2613121192 S C:7:0005:0 80 06 0100 0000 0012 18 <
d2263a80 2613121399 C:7:0005:0 18 = 12010002 00000040 21123432 00000102 0301
```