
## Human Interface Devices

Devices such as keyboards and mice are called *human interface devices* (HIDs). Take a look at the section "USB and Bluetooth Keyboards" in Chapter 7, "Input Drivers," for a discussion on the USB HID class.

## Bluetooth

A USB-Bluetooth dongle is a quick way to Bluetooth-enable your computer so that it can communicate with Bluetooth-equipped devices such as cell phones, mice, or handhelds. Chapter 16 discusses the USB Bluetooth class.

## Gadget Drivers

In a typical usage scenario, an embedded device connects to a PC host over USB. Embedded computers usually belong to the device side of USB, unlike PC systems that function as USB hosts. Because Linux runs on both embedded and PC systems, it needs support to run on either end of USB. The USB Gadget project brings USB device mode capability to embedded Linux systems. Bus 3 of the embedded Linux device in Figure 11.2 can, for example, use a **gadget driver** to let the device function as a mass storage drive when connected to a host computer.

Before proceeding, let's briefly look at some related terminology. The USB controller at the device side is variously called a *device controller, peripheral controller, client controller*, or *function controller*. The terms **gadget** and **gadget driver** are commonly used rather than the heavily overloaded words *device* and *device driver*.

USB gadget support is now part of the mainline kernel and contains the following:

- Drivers for USB device controllers integrated into SoC families such as Intel PXA, Texas Instruments OMAP, and Atmel AT91. These drivers additionally provide a *gadget API* that gadget drivers can use.
- Gadget drivers for device classes such as storage, networking, and serial converters. These drivers answer to their class when they receive enumeration requests from host-side software. A storage gadget driver, for example, identifies itself as a class 0x08 (mass storage class) device and exports a storage partition to the host. You can specify the associated block device node or filename via a module-insertion parameter. Because the exported region has to appear to the host as a mass storage device, the gadget driver implements the SCSI interactions required by the USB mass storage protocol. Gadget drivers are also available for Ethernet and serial devices.
- A skeletal gadget driver, `drivers/usb/gadget/zero.c`, that you may use to test device controller drivers.

Gadget drivers use the services of the gadget API provided by device controller drivers. They populate a `usb_gadget_driver` structure and register it with the kernel using `usb_gadget_register_driver()`. Hardware specifics are hidden inside the gadget API implementation offered by individual device controller drivers, so the gadget drivers themselves are hardware independent.

*Documentation/DocBook/gadget.tmpl* provides an overview of the gadget API. Have a look at http://linux-usb.org/gadget/ for more on the gadget project.

## Debugging

A USB bus analyzer magnifies the goings-on in the bus and is useful for debugging low-level problems. If you can't get hold of an analyzer, you might be able to make do with the kernel's soft USB tracer, `usbmon`. This tool captures traffic between USB host controllers and devices. To collect a trace, read the `debugfs`[^1] file `/sys/kernel/debug/usbmon/Xt`, where X is the bus number to which your device is connected.

[^1]: An in-memory filesystem to export kernel debug data to user space.

For example, consider a USB disk connected to a PC. From the associated "T:" line in `/proc/bus/usb/devices`, you can see that the drive is attached to bus 1:

```
T :  Bus=01  Lev=01  Prnt=01  Port=03  Cnt=01  Dev#= 2  S pd=480  MxCh= 0
```

Ensure that you have enabled `debugfs` (`CONFIG_DEBUG_FS`) and `usbmon` (`CONFIG_USB_MON`) support in your kernel. This is a snapshot of usbmon output while copying a file from the disk:

```
Code View:
bash> mount -t debugfs none_debugs /sys/kernel/debug/
bash> cat /sys/kernel/debug/usbmon/1u
...
ee6a5c40 3718782540 S B1:1:002:1 --115 20480 <
ee6a5cc0 3718782567 S B1:1:002:1 --115 65536 <
ee6a5d40 3718782595 S B1:1:002:1 --115 36864 <
ee6a5d40 3718788189 C B1:1:002:1 0 20480 = 0f4a6801 118498f\ 15c60500 01680106
5e846801 608498fe 6f280087 68000000
ee6a5cc0 3718800994 C B1:1:002:1 0 65536 = 118498fe 15c60500\ 01680106 5e846801
608498fe 6f280087 68000000 00884800
ee6a5d40 3718801001 C B1:1:002:1 0 36864 = 13608498 fe4f4a01\ 00514a01 006f2800
87680000 00008848 00000100 b7f00100
...
```

Each output line starts with the URB address, followed by an event timestamp. An S in the next column indicates URB submission, and a C announces a callback. The following field has the format `URBType:Bus#:DeviceAddress:Endpoint#`. In the preceding output, an `URBType` of `B1` stands for a bulk URB in the IN direction. After this, usbmon dumps the URB status, data length, a data tag (= or < in the preceding output), and the data words (if the tag is =). The last three lines in the preceding output are callbacks associated with bulk URBs submitted in earlier lines. You can match the callbacks with the related submissions using the URB addresses. `Documentation/usb/usbmon.txt` details usbmon syntax and contains example code to parse the output into human readable form.

If you turn on Device Drivers → USB Support → USB Verbose Debug Messages during kernel configuration, the kernel will emit the contents of all `dev_dbg()` statements present in the USB subsystem.

You can glean device and bus specific information from the USB filesystem (usbfs) node, `/proc/bus/usb/devices`. And as we discuss in Chapter 19, "Drivers in User Space," usbfs also lets you implement USB device drivers in user space. Even when the final destination of your USB driver is inside the kernel, starting with a user-space driver can ease debugging and testing.

The linux-usb-devel mailing list is the forum to discuss questions related to USB device drivers. Visit https://lists.sourceforge.net/lists/listinfo/linux-usb-devel for subscription and archive retrieval information. Read www.linux-usb.org/ushtest for ideas on USB testing.

The home page of the Linux-USB project is www.linux-usb.org. You may download the USB 2.0 specification, OTG supplement, and other related standards from www.usb.org/developers/docs.

## Looking at the Sources

The USB core layer lives in `drivers/usb/core/`. This directory also contains URB manipulation routines and the usbfsc implementation. The hub driver and khubd are part of `drivers/usb/core/hub.c`. The `drivers/usb/host/` directory contains host controller device drivers. USB-related header definitions reside in `include/linux/usb/*.h`. The usbmon tracer is in `drivers/usb/mon/`. Look inside `Documentation/usb/` for Linux-USB documentation.

USB class drivers stay in various subdirectories under `drivers/usb/`. The mass storage driver `drivers/usb/storage/`, in tandem with the SCSI subsystem `drivers/scsi/`, implements the USB mass storage protocol. The `drivers/input/` [^2] directory tree includes drivers for USB input devices such as keyboards and mice; `drivers/usb/serial/` has drivers for USB-to-serial converters; `drivers/usb/media/` supports USB multimedia devices; `drivers/net/usb/` [^3] has drivers for USB Ethernet dongles; and `drivers/usb/misc/` contains drivers for miscellaneous USB devices such as LEDs, LCDs, and fingerprint sensors. Look at `drivers/usb/usb-skeleton.c` for a starting point driver template if you can't zero in on a closer match.

[^2]: Before the 2.6.22 kernel release, USB input device drivers used to reside in `drivers/usb/input/`.
[^3]: Before the 2.6.22 kernel release, USB network device drivers used to reside in `drivers/usb/net/`.

The USB gadget subsystem is in `drivers/usb/gadget/`. This directory contains USB device controller drivers, and gadget drivers for mass storage (`file_storage.c`), serial converters (`serial.c`), and Ethernet networking (`ether.c`).

Table 11.3 contains the main data structures used in this chapter and their location in the source tree. Table 11.4 lists the main kernel programming interfaces that you used in this chapter along with the location of their definitions.

**Table 11.3. Summary of Data Structures**

| Data Structure | Location | Description |
| :--- | :--- | :--- |
| `urb` | `include/linux/usb.h` | Centerpiece of the USB data transfer mechanism |
| `pipe` | `include/linux/usb.h` | Address element of a URB |
| `usb_device_descriptor` `usb_config_descriptor` `usb_interface_descriptor` `usb_endpoint_descriptor` | `include/linux/usb/ch9.h` | Descriptors that hold information about a USB device |
| `usb_device` | `include/linux/usb.h` | Representation of a USB device |
| `usb_device_id` | `include/linux/mod_devicetable.h` | Identity of a USB device |
| `usb_driver` | `include/linux/usb.h` | Representation of a USB client driver |
| `usb_gadget_driver` | `include/linux/usb_gadget.h` | Representation of a USB gadget driver |

## Table 11.4. Summary of Kernel Programming Interfaces
