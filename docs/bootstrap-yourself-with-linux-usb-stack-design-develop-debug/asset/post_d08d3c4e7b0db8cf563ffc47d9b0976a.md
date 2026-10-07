
## More Reading

After mapping the platform, the driver obtains control of the device controller hardware. The probe routine now initialize control of the device controller hardware and set it up for USB activity. The other part of the device routine is specific to the device controller. You can explore it from the source available in the kernel.

```
ret = request_irq(irq, r8a66597_irq, IRQ_DISABLED | IRQ_SHARED,
udc_name, r8a66597);
```

The platform IRQ is mapped to the PDC driver handler r8a66597_irq using the request_irq interface function. Once the IRQ is successfully mapped, the PDC driver starts receiving IRQ and handles USB transfers.

## SUMMARY

The peripheral device controller driver is the only layer of the gadget driver directly interacts with the USB device hardware. Although the implementation framework is the same, it varies for each USB controller and the way it is integrated with the platform. You have to carefully read the data sheet of the USB controller and the platform hardware details before implementing this driver layer. In the next chapter, you read about the gadget layer, which sits on top of the PDC layer. The gadget layer handles USB-specific device operations and is independent of the USB controller hardware being used.

## MORE READING

You can collect more information on the Linux platform driver framework from the Linux kernel documentation Documentation/driver-model/platform.txt. When your platform adds extra glue logic to interact with the device controller hardware, additional driver frameworks such as GPIO are required to control the hardware. You can read more about the GPIO framework from the Linux kernel documentation Documentation/gpio.txt.

## CHAPTER 13

## GADGET DRIVER

### In This Chapter

- Bootstrap Essentials: Gadget Driver
- Gadget Driver: Design
- Gadget Driver: Implementation

The gadget driver is an important infrastructure in the USB gadget subsystem. It is built in a flexible way that allows the upper class or the functional driver to manage the system effectively. The gadget framework is the core of the Linux USB gadget subsystem; it provides a framework for the USB device framework, as described by USB Specification (Chapter 9). It also performs other USB device management operations that are specific to the implementation. The gadget driver provides the framework required for a USB device to operate and expects intelligence of configuring the device from the gadget driver or the upper layer. Such a design offers flexibility to develop class drivers with different device configurations and functionality.

This chapter first explores the essential gadget data structures defined by the gadget driver. From there, it discusses the gadget framework’s flow of activity and the way other layers use the gadget framework. Finally, this chapter analyzes a gadget driver implementation with a practical example.

![](img/779a74a6577501a55983f193067274a3_177_0.png)

## BOOTSTRAP ESSENTIALS: GADGET DRIVER

The gadget driver relies on four major data structures: struct usb_gadget to represent a gadget device, struct usb_ep to manage the device hardware, struct usb_gadget_driver to manage the device function, struct usb_request to manage USB transfers. These data structures hold key information for the gadget layer and methods that extend the gadget infrastructure to other layers. These data structures and methods are defined in include/linux/usb/gadget.h of the Linux kernel source. The next section explains the methods that these key data structures extend.

## USB Gadget Data Structure and Methods

The struct usb_gadget represents the USB device within the gadget layer. struct usb_gadget uses methods to perform hardware-specific operations and maintains gadget-related information, such as endpoint lists. Thus, this data structure acts as an abstraction of the hardware. Its members are most read only.

```
struct usb_gadget {
    const struct usb_gadget_ops *ops;
    struct usb_ep *ep0;
    struct list_head ep_list;
    enum usb_device_speed speed;
    unsigned is_dualspeed:1;
    unsigned is_otg:1;
    unsigned is_a_peripheral:1;
    unsigned b_hnp_enable:1;
    unsigned a_hnp_support:1;
    unsigned a_lt_hnp_support:1;
    const char *name;
    struct device dev;
};
```

Notice that struct usb_gadget defines only a basic set of gadget information. When you are developing a gadget layer for a USB device, you might need additional gadget-related information. You can define a data structure that is a superset of struct usb_gadget, which can hold additional information.

The struct usb_gadget declares the struct usb_gadget_ops member to export the hardware-specific operations. These gadget operations extend gadget features to the upper layers through wrapper functions. The following section details the gadget operations.

```
struct usb_gadget_ops {
 int (*frame)(struct usb_gadget *);
 int (*wakeup)(struct usb_gadget *);
 int (*self_powered)(struct usb_gadget *, int is_selfpowered);
 int (*vbus_session)(struct usb_gadget *, int is_active);
 int (*vbus_draw)(struct usb_gadget *, unsigned mA);
 int (*pullup)(struct usb_gadget *, int is_on);
 int (*ioctl)(struct usb_gadget *, unsigned code, unsigned long param);
};
```

- * (*frame)(struct usb_gadget *)
This callback returns the current frame number.

- * (*wakeup)(struct usb_gadget *)
This callback sends a notification to the host. The gadget driver provides an interface to access the callback. A successful wakeup returns 0, and a failure returns a negative value.

- * (*self_powered)(struct usb_gadget *, int is_selfpowered)
This callback sets the self-powered state. The gadget layer provides an interface to access the callback. A successful self-powered-state change returns 0.

- * (*pullup)(struct usb_gadget *, int is_on)
This callback controls the pull-up. The gadget layer provides an interface to access the callback. A successful pull-up returns 0, and a failure returns a negative value.

- * (*ioctl)(struct usb_gadget *, unsigned code, unsigned long param)
This callback handles input/output control (IOCTL). A successful operation returns 0, and a failure returns a negative value.

## Endpoint Data Structure and Methods

The next important functionality in the gadget layer is endpoint management. The endpoint data structure extends methods to manage the endpoints. One of the foremost and important functionalities is data management. The struct usb_ep extends a layer for data management and certain buffer management that is specific to the endpoint. Endpoint available in the hardware, each endpoint is assigned an instance of the struct usb_ep data structure.

```
struct usb_ep {
    void *driver_data;
    const char *name;
    const struct usb_ep_ops *ops;
    struct list_head ep_list;
    unsigned maxpacket:16;
};
```

The struct usb_ep declares a struct usb_ep_ops member to export endpoint-specific operations. These endpoint operations allow the lower layers to control and manage an endpoint. The following section details the endpoint operations.

```
struct usb_ep_ops {
    int (*enable)(struct usb_ep *ep,
        const struct usb_endpoint_descriptor *desc);
    int (*disable)(struct usb_ep *ep);
    struct usb_request *t (*alloc_request)(struct usb_ep *ep,
        gfp_t gfp_flags);
    void (*free_request)(struct usb_ep *ep, struct usb_request *req);
    int (*queue)(struct usb_ep *ep, struct usb_request *req,
        gfp_t gfp_flags);
    int (*dequeue)(struct usb_ep *ep, struct usb_request *req);
    int (*halt)(struct usb_ep *ep, int value);
    int (*set_wedge)(struct usb_ep *ep);
    int (*fifo_status)(struct usb_ep *ep);
    void (*fifo_flush)(struct usb_ep *ep);
};
```

- * int (*enable)(struct usb_ep *ep, const struct usb_endpoint_descriptor *desc)
This callback provides the necessary infrastructure to configure an endpoint by upper class driver layers. This is required when a configuration is set or interfaces are changed and requires successful setting up of endpoint for transfers. A successful endpoint enable returns 0, and a failure returns a negative code. The gadget layer provides an interface function usb_ep_enable to access the callback.
