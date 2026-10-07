
# Chapter 8 = Hub

![](img/779a74a6577501a55983f193067274a3_122_0.png)

**Figure 8.3**
A generic breakdown of the Linux USB hub framework.

One important functionality of the hub framework is management of hub events and state changes through khubd. During initialization, this framework creates a kernel thread (khubd) that waits in an infinite loop to manage hub events. The framework also implements the hub driver that probes and identifies hub devices. The framework contributes to device enumeration and manages the enumeration state machine. It also provides infrastructure support for runtime power management, as discussed in the previous chapter. The subsequent sections explore the sequence of activities that are internal to the hub framework.

The hub framework defines a `struct usb_driver` as part of the uscore, which represents a USB hub device. The driver is registered with the uscore module using the `usb_register` interface function. The probe routine identifies a hub and successfully configures the device, after which you can manage the hub device.

```c
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

# Linux USB Hub Framework

![](img/779a74a6577501a55983f193067274a3_123_0.png)

**Figure 8.4**
Initialization sequence of Linux USB hub framework.

Figure 8.4 illustrates the activities that occur during the hub framework initialization. The uscore module starts the hub initialization, which involves the hub framework registering the hub USB driver with the uscore module and starting the khubd to manage the events.

Another important feature used at the application level is the USB device reset, which is managed in the hub framework. Figure 8.5 illustrates a simplified reset sequence whose key functions are represented in the sequence flow. The hub driver invokes the `pre_reset` callback before resetting the device and invokes the `post_reset` callback; the driver provides both. The driver learns about the reset through these callbacks.

Another important aspect that the hub framework manages is enumeration and device state management. Figure 8.6 illustrates the sequence of activities during the enumeration process.

The process starts with a state change in the hub's port, which the `hub_port_connect_change` function manages. After successful enumeration, the hub framework adds the device to the kernel through the `device_add` interface function of the kernel device framework. The driver that matches the device takes control, and the device is brought to the configuration state. The enumeration process for OTG devices is part of this path you can explore to improve the sequence.

The core functionality of the hub framework is the handling of events. Figure 8.7 illustrates the flow of activities inside the khubd while handling events.

The khubd waits in an infinite loop for any hub activity, which is notified through a `kick_khubd` interface routine. This allows the hub to come out of the wait state and process the new event using `hub_events`. After successful processing, the khubd thread hub_thread again waits for new events.

This section captured the basic functionalities of the hub framework.

![](img/779a74a6577501a55983f193067274a3_125_0.png)

**Figure 8.6**
A simplified enumeration sequence involving the hub.

# Chapter 8 = Hub

![](img/779a74a6577501a55983f193067274a3_124_0.png)

**Figure 8.5**
A simplified reset sequence involving the hub.

![](img/779a74a6577501a55983f193067274a3_126_0.png)

**Figure 8.7**
A simplified event flow.

## Summary

The hub framework is a critical component of the Linux USB subsystem, managing the lifecycle and state of USB hubs. By utilizing the `khubd` thread, it ensures that hub events are handled asynchronously. The framework also handles device enumeration, reset sequences, and power management, providing a robust infrastructure for USB-based communication.
