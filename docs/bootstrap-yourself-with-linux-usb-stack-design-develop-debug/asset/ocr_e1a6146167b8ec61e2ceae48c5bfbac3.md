# Linux USB Gadget Subsystem

depends on USB
default y

# Power Management

A USB host system can suspend the USB devices when the bus has no activity.
The Linux USB host system provides an option to suspend the devices and
enables runtime power management. The following configuration from the
drivers/usb/core/Kconfig file allows you to configure the USB power as part of
the kernel.

```
config USB_SUSPEND
bool "USB runtime power management (suspend/resume and wakeup)"
depends on USB && PM_RUNTIME
```

# Test Infrastructure

The host infrastructure also provides test facilities that enable you to test certain
host and device facilities. The following configuration from the drivers/
misc/Kconfig file allows you to configure the USB test feature part of the kernel
and generate usstest.ko.

```
config USB_TEST
tistrate "USB testing driver"
depends on USB
```

# LINUX USB Gadget Subsystem

The next key framework of the Linux USB subsystem is the gadget driver
framework or the driver framework for the USB device controller, device
protocol implementation, and functional drivers of a USB device. The frame-
work also implements the debug and gadget file system. Figure 3.10 provides an
architectural view of the Linux gadget subsystem.

The USB controller driver implements the driver module for the USB device
controller, which acts mainly as a hardware abstraction layer exporting hardware
features to the above gadget layers. The gadget layer implements the USB protocol
framework that interfaces the device driver layer and the class layer, such as
storage. The class driver layer implements the functional aspect of the USB device.

The drivers/usb/gadget/Kconfig configuration file contains the various options
to select gadget framework features. You can enable the USB gadget driver from