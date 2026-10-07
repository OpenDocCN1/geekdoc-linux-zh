# BOOTSTRAP ESSENTIALS: CLASS DRIVERS

The class driver is responsible for managing the functional aspects of the USB device determined by the USB descriptors. The important data structures that the class driver uses the descriptor data structures. These data structures are defined in the include/linux/usb/ch9.h file of the kernel source.

The data structures struct usb_device_descriptor, struct usb_config_descriptor, struct usb_interface_descriptor, and struct usb_endpoint_descriptor are passed on to the gadget driver by the class driver. The descriptor as defined by Chapter 9 of the USB specification allows a description of the device to the host.

```
struct usb_device_descriptor {
	__u8 bLength;
	__u8 bDescriptorType;
	__le16 bcdUSB;
	__u8 bDeviceClass;
	__u8 bDeviceSubClass;
	__u8 bDeviceProtocol;
	__u8 bMaxPacketSize;
	__le16 idVendor;
	__le16 idProduct;
	__le16 bcdDevice;
	__u8 iManufacturer;
	__u8 iProduct;
	__u8 iSerialNumber;
	__u8 bNumConfigurations;
} __attribute__((packed));
struct usb_config_descriptor {
	__u8 bLength;
	__u8 bDescriptorType;
	__le16 wTotalLength;
	__u8 bNumInterfaces;
	__u8 bConfigurationValue;
	__u8 iConfiguration;
	__u8 bmAttributes;
	__u8 bMaxPower;
} __attribute__((packed));
struct usb_interface_descriptor {
	__u8 bLength;
```