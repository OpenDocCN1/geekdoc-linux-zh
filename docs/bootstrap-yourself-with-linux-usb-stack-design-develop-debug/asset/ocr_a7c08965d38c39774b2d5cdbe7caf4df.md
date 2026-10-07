# Bootstrap Essentials: Linux Hub

The bNbrPorts member contains information on the number of downstream-facing ports the hub supports.

```
__u8 bNbrPorts;
__u16 wHubCharacteristics;
__u8 bPwOn2PwrGode;
__u8 bHubContCurrent;
```

The DeviceRemovable member variable indicates whether a port has a removable device attached. The Linux USB framework defines USB_MAXCHILDREN in include/usb.h. The Linux USB framework supports 31 devices.

```
__u8 DeviceRemovable[(USB_MAXCHILDREN + 1) / 8];
__u8 PortPwrMask[(USB_MAXCHILDREN + 1) / 8];
__attribute__((packed));
```

A hub is responsible for managing full-/low-speed devices when operating in high-speed mode; the Transaction Translator (TT) portion of the hub performs this function. This data structure is visible only in the hub framework to hub and high-speed host controller driver (HCD) framework.

```
struct usb_bt {
struct hub variable represents an upstream high-speed hub.
struct usb_device
    *hub;
The multimember variable indicates the usage of TT from the HCD framework.
int
    multi;
the think_time member variable holds the Think Time value in nanoseconds as defined by USB Hub specification.

    unsigned think_time;
    spinlock_t lock;
    struct list_head clear_list;
    struct work_struct clear_work;
};
```

The Linux hub framework uses a data structure within the framework to manage events and other requests. Figure 8.2 illustrates the events, change information, and control information for the device. The struct usb_hub defined in drivers/core/hub.c provides an infrastructure to store the information represented in the figure. The hub daemon khud of the hub framework manages this information.