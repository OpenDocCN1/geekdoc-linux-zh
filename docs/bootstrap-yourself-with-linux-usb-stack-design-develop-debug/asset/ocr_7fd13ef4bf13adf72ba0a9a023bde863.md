# Chapter 3 = Overview of the Linux USB Subsystem

Linux USB subsystem, the usbcore module implements the debug infrastructure, power management, USB file systems, and USB host protocol. Some of the USB class specifications and debug monitoring tools are implemented as part of the USB host system.

The configuration and selection of the kernel modules are based on the Kconfig files. The root configuration file for the USB subsystem is drivers/usb/Kconfig. To enable USB support in the kernel, the configuration option is available in Device Drivers, USB Support. The following snap of drivers/usb/Kconfig file provides the menu for USB support. The USB support depends on the IOMEM (Input/Output memory part of lib/Kconfig) option, which should be enabled for USB to be supported.

The following configuration from drivers/usb/Kconfig shows the dependency of USB on the IOMEM.

```
menuconfig USB_SUPPORT
bool "USB support"
depends on HAS_IOMEM
def y
```

Figure 3.2 illustrates the USB support option when you make menuconfig to configure the kernel.

The USB support menu is enabled by default, as are the EHCI and OHCI menus. Subsequent menu entries depend on these flags.

The following configuration from drivers/usb/Kconfig shows that host-side USB depends on having a host controller support.

```
config USB_ARCH_HAS_HCD
boolean
default y if USB_ARCH_HAS_OHCI
default y if USB_ARCH_HAS_EHCI
```

The following sections explain key configuration options that are part of the USB host functionality in the Linux USB subsystem.

# USB HCD Driver Menu

A USB host controller implementation is based on specifications EHCI, UHCI, or OHCI, or sometimes it's customized for certain embedded controllers that are