# Chapter 8 = Hub

![](bbox=[0.078, 0.093, 0.731, 0.269])

**Figure 8.3**
A generic breakdown of the Linux USB hub framework.

One important functionality of the hub framework is management of hub events and state changes through khubd. During initialization, this framework creates a kernel thread (khubd) that waits in an infinite loop to manage hub events. The framework also implements the hub driver that probes and identifies hub devices. The framework contributes to device enumeration and manages the enumeration state machine. It also provides infrastructure support for runtime power management, as discussed in the previous chapter. The subsequent sections explores the sequence of activities that are internal to the hub framework.

The hub framework defines a struct usb_driver as part of the uscore, which represents a USB hub device. The driver is registered with the uscore module using the usb_register interface function probe routine identifies a hub and successfully configures the device, after which you can manage the hub device.

```
static struct usb_driver hub_driver = {
    .name = "hub",
    .probe = hub_probe,
    .disconnect = hub_disconnect,
    .suspend = hub_suspend,
    .resume = hub_resume,
    .reset_reset = hub_reset_reset,
    .pre_reset = hub_pre_reset,
    .post_reset = hub_post_reset,
    .ioctl = hub_ioctl,
    .id_table = hub_id_table,
    .supports_autosuspend = 1,
};
```