# # Class Drivers

The USB specification introduces the concept of device classes and describes the functionality of each class driver. Examples of standard device classes include mass storage, networking, hubs, serial converters, audio, video, imaging, modems, printers, and human interface devices (HIDs). Class drivers are generic and let you plug and play a wide array of cards without the need for developing and installing drivers for every single device. The Linux-USB subsystem includes support for major class drivers.

Each USB device has a class and a subclass code. The mass storage class (`0x08`), for example, supports subclasses such as compact disc (`0x02`), tape (`0x03`), and solid-state storage (`0x06`). As you saw previously, device drivers populate the `usb_device_id` structure with the classes and subclasses they support. You can glean a device's class and subclass information by looking at the `:*` lines in the `/proc/bus/usb/devices` output.

Let's take a look at some important class drivers.

# ## Mass Storage

In USB parlance, mass storage refers to USB hard disks, pen drives, CD-ROMs, floppy drives, and similar storage devices. USB mass storage devices adhere to the Small Computer System Interface (SCSI) protocol to communicate with host systems. Block access to USB storage devices is hence routed through the kernel's SCSI subsystem. Figure 11.4 provides you an overview of the interaction between USB storage and SCSI subsystems. As shown in the figure, the SCSI subsystem is architected into three layers:

+   1. Top-level drivers for devices such as disks (`sd.c`) and CD-ROMs (`sr.c`)

+   2. A middle-level layer that scans the bus, configures devices, and glues top-level drivers to low-level drivers

+   3. Low-level SCSI adapter drivers

# **Figure 11.4. USB mass storage and SCSI.**

![](bbox=[0.42, 0.89, 0.54, 0.9])