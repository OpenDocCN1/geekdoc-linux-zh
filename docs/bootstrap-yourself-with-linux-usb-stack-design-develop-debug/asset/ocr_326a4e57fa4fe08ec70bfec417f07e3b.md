# Bootstrap Essentials: Gadget Driver 63

features to the upper layers through wrapper functions. The following section details the gadget operations.

```
struct usb_gadget_ops {
 int (*frame)(struct usb_gadget *);n int (*wakeup)(struct usb_gadget *);n int (*self_powered)(struct usb_gadget *, int is_selfpowered);
 int (*vbus_session)(struct usb_gadget *, int is_active);
 int (*vbus_draw)(struct usb_gadget *, unsigned mA);
 int (*pullup)(struct usb_gadget *, int is_on);
 int (*ioctl)(struct usb_gadget *, unsigned code, unsigned long param);
};
```

+   * (*frame)(struct usb_gadget *)
This callback method returns the current frame number if the controller supports retrieval of the USB frame number. The usb_gadget_frame_number acts as the interface function. When the capability is not available, a negative value is returned.

+   * (*wakeup)(struct usb_gadget *)
This callback method sends a wakeup notification to the USB host that the device hardware is connected to. The usb_gadget_wakeup serves as an interface function to the callback that performs the necessary hardware-specific operation. A device supporting this feature must inform the USB host through the USB descriptors. If the operation is successful, 0 is returned; if the operation fails, a negative value is returned.

+   * (*self_powered)(struct usb_gadget *, int is_selfpowered)
This callback method sets the device as self-powered. Interface functions usb_gadget_set_self_powered and usb_gadget_clear_self_powered enable and disable the device to and from the self-powered state, respectively. This operation affects the device status and is indicated by the peripheral device controller (PDC) driver. If the operation is successful, 0 is returned; if the operation fails, a negative value is returned.