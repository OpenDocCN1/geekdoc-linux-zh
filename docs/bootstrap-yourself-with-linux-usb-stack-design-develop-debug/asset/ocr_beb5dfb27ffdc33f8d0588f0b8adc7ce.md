# Chapter 12 = Peripheral Device Controller Driver

From a top-level overview, the PDC driver's major functionality is to allocate necessary resources such as memory and interrupt requests (IRQs) when the platform probe for the device is successful and release the allocated resources when the device is disconnected. Thus, a successful PDC driver allows the USB controller to be ready for other USB driver leafs and frees up the platform resources.

This chapter further explores the Linux platform driver framework that you should know before developing PDC driver. The subsequent sections explore the functional breakdown of the PDC driver, the activity flow of the driver, and a sample PDC driver implementation.

# BOOTSTRAP ESSENTIALS: PLATFORM DRIVER

The USB device controller hardware connects to the platform using proprietary interfaces. It is important to develop the device driver with minimum complexity. The Linux platform driver is a pseudo-bus generic driver model that connects to proprietary interfaces with a simple driver framework. The platform driver framework offers direct access to the platform hardware bus. Most of the USB PDC driver is developed based on the platform driver framework. The following sections explore the basics of the platform driver framework to enable you to understand and develop a USB PDC driver.

The linux/platform_device.h file contains definitions and declarations of the platform driver framework. The platform driver exports its functionality through two major data structures: the struct platform_device and the struct platform_driver.

The platform_device data structure represents the device with members to identify the device and fields to represent sets of resources such as IRQ and memory allocated to the device. The Name field helps to identify the resources allocated once the probing is successful.

```
struct platform_device {
    const char *name;
    int id;
    struct device dev;
    u32 num_resources;
    struct resource * resource;
};
```