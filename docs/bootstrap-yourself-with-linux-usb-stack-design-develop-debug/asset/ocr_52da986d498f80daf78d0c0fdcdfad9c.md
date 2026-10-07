# Linux USB Host Subsystem

```
*** USB Device Class drivers ***
<M> USB Modem (CDC ACM) support
```

Figure 3.9
menuconfig option displaying USB CDC option.

Sometimes you need to add serial console support to your device to emulate a terminal console over serial port. The following option enables you to set serial console support.

```
config USB_SERIAL_CONSOLE
    bool "USB Serial Console device support"
	depends on USB_SERIAL=y
```

When a device does not have a serial driver of its own, enable this generic driver so that a host can detect it at runtime. You can specify insmod usbserial vendor=V-ID product=P-ID, where V-ID and P-ID are the vendor and product ID of your device.

```
config USB_SERIAL_GENERIC
    bool "USB Generic Serial Driver"
```

When it’s configured to generate as a module, the makefile generates usserial.ko, allowing you to load and unload the module dynamically.

# CDC Ethernet Support

The other important class of USB is the Ethernet class, which is available in most of the embedded systems that support USB. This feature is needed only in a USB host to support such devices that provide CDC Ethernet support. The following option enables a USB host to support USB CDC devices.

Figure 3.9 illustrates the CDC class menu when you run a menuconfig, which is outside the USB host.

The following configuration from drivers/net/usb/Kconfig file provides the necessary menu options to configure the USB host CDC support.

```
#
# USB Network devices configuration
#
comment "Networking support is needed for USB Network Adapter support"
	depends on USB && !NET

n
```