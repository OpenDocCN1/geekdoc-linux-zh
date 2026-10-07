# Chapter 8 = Hub

![](bbox=[0.082, 0.105, 0.918, 0.328])

```
struct usb_hub {
--cut-
--cut-
    struct list_head        event_list;
    unsigned long               event_bits[1];
    unsigned long               change_bits[1];

    unsigned long               busy_bits[1];

    unsigned long               removed_bits[1];

    struct usb_hub_descriptor *descriptor;
    struct usb_tt                tt;

--cut-
--cut-
);
```

**Figure 8.2**nHub events and system software relationship. (REF Figure 11-20 USB 2.0 Specification)

Having covered the essential data structures for the hub framework, the following section explores the key exported interface functions of the Linux hub framework.

+   - void usb_set_device_state(struct usb_device *udev, enum usb_device_state new_state)

This interface function allows usbcore and the host controller driver (HCD) framework to change a device's current state to the specified