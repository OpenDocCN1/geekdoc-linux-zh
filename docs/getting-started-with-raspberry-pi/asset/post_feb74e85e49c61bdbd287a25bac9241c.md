
## Bus Speeds

USB supports three operational speeds. The original USB 1.0 specification supports 1.5Mbps, referred to as low-speed USB. USB 1.1, the next version of the specification, handles 12Mbps, called full-speed USB. The current level of the specification is USB 2.0, which supports 480Mbps, or high-speed USB. USB 2.0 is backward-compatible with the earlier versions of the specification. Peripherals such as USB keyboards and mice are examples of low-speed devices, and USB storage drives are examples of full-speed and high-speed devices. Today's PC systems are USB 2.0-compliant and allow all three target speeds, but some embedded controllers adhere to USB 1.1 and support only full-speed and low-speed modes of operation.

## Host Controllers

USB host controllers conform to one of a few standards:

-   **Universal Host Controller Interface (UHCI):** The UHCI specification was initiated by Intel, so your PC is likely to have this controller if it's Intel-based.
-   **Open Host Controller Interface (OHCI):** The OHCI specification originated from companies such as Compaq and Microsoft. An OHCI-compatible controller has more intelligence built into hardware than UHCI, so an OHCI HCD is relatively simpler than a UHCI HCD.
-   **Enhanced Host Controller Interface (EHCI):** This is the host controller that supports high-speed USB 2.0 devices. EHCI controllers usually have either a UHCI or OHCI companion controller to handle slower devices.
-   **USB OTG controllers:** They are getting increasingly popular in embedded microcontrollers. With OTG support, each communicating end can act as a *dual-role device* (DRD). By initiating a dialog using the *Host Negotiation Protocol* (HNP), a DRD can switch itself to host mode or device mode based on the desired functionality.

In addition to these mainstream USB host controllers, Linux supports a few more controllers. An example is the HCD for the ISP116x chip.

Host controllers have a built-in hardware component called the *root hub*. The root hub is a virtual hub that sources USB ports. The ports, in turn, can connect to external or internal physical hubs and source more ports, yielding a tree topology.

## Transfer Types

Data exchange with a USB device can be one of four types:

-   Control transfers, used to carry configuration and control information
-   Bulk transfers that ferry large quantities of time-insensitive data
-   Interrupt transfers that exchange small quantities of time-sensitive data
-   Isochronous transfers for real-time data at predictable bit rates

A USB storage drive, for example, uses control transfers to issue disk access commands and bulk transfers to exchange data. A keyboard uses interrupt transfers to carry key strokes within predictable delays. A device that needs to stream audio data in real time uses isochronous transfers. The responsibilities of the four transfer types for USB Bluetooth devices are discussed in the section "Device Example: USB Adapter" in Chapter 16, "Linux Without Wires."

## Addressing

Each addressable unit in a USB device is called an *endpoint*. The address assigned to an endpoint is called an *endpoint address*. Each endpoint address has an associated data transfer type. If an endpoint is responsible for bulk data transfer, for example, it’s called a *bulk endpoint*. Endpoint address 0 is used exclusively for device configuration. A control pipe is attached to this endpoint for device enumeration (see the section "Enumeration").

An endpoint can be associated with upstream or downstream data transfer. Data arriving upstream from a device is called an **IN** transfer, whereas data flowing downstream to a device is an **OUT** transfer. **IN** and **OUT** transfers own separate address spaces. So, you can have a bulk **IN** endpoint and a bulk **OUT** endpoint answering to the same address.

USB resembles I²C on some counts and PCI on others as summarized in Table 11.1. USB’s device addressing is similar to I²C, while it supports hotplugging like PCI. USB device addresses, like standard I²C, do not consume a portion of the CPU’s address space. Rather, they reside in a private space ranging from 1 to 127.

### Table 11.1. USB’s Similarities with I²C and PCI

| Similarities with I²C | Similarities with PCI |
| :--- | :--- |
| USB and I²C are master-slave protocols. | Devices can be hotplugged. |
| Device addresses reside in a private 7-bit space. | Device driver architecture resembles PCI drivers. Both classes of drivers own `probe()` / `disconnect()` methods and ID tables identifying the devices they support.<sup>[1]</sup> |
| Device-resident memory is not mapped to the CPU’s memory or I/O space, so it does not consume CPU resources. | Supports high speeds. Slower than PCI, however. See Table 10.1 in Chapter 10, “Peripheral Component Interconnect,” for the speeds supported by different members of the PCI family. |
| | USB host controllers, like PCI controllers, usually have built-in DMA engines that can master the bus. |
| | Supports multifunction devices. USB supports interface descriptors per function. Each PCI device function has its own device ID and configuration space. |

<sup>[1]</sup> `disconnect()` is called `remove()` in PCI parlance.

## Linux-USB Subsystem

Look at Figure 11.3 to understand the architecture of the Linux-USB subsystem. The constituent pieces of the subsystem are as follows:

-   The USB core. Like the core layers of driver subsystems that you saw in previous chapters, the USB core is a code base consisting of routines and structures available to HCDs and client drivers. The core also provides a level of indirection that renders client drivers independent of host controllers.
-   HCDs that drive different host controllers.
-   A hub driver for the root hub (and physical hubs) and a helper kernel thread `khubd` that monitors all ports connected to the hub. Detecting port status changes and configuring hotplugged devices is time-consuming and is best accomplished using a helper thread for reasons you learned in Chapter 3, "Kernel Facilities." The `khubd` thread is asleep by default. The hub driver wakes `khubd` whenever it detects a status change on a USB port connected to it.
-   Device drivers for USB client devices.
-   The USB filesystem `usbfs` that lets you drive USB devices from user space. We discuss user mode USB drivers in Chapter 19, "Drivers in User Space."

![](img/07cc6f9c8c74622020874f66bfb53dc4_296_0.png)

For end-to-end operation, the USB subsystem calls on various other kernel layers for assistance. To support USB mass storage devices, for example, the USB subsystem works in tandem with SCSI drivers, as shown in Figure 11.3. To drive USB-Bluetooth keyboards, the stakeholders are fourfold: the USB subsystem, the Bluetooth layer, the input subsystem, and the tty layer.

## Driver Data Structures

When you write a USB client driver, you have to work with several data structures. Let's look at the important ones.

### The usb_device Structure

Each device driver subsystem relies on a special-purpose data structure to internally represent a device. The `usb_device` structure is to the USB subsystem, what `pci_dev` is to the PCI layer, and what `net_device` is to the network driver layer. `usb_device` is defined in `include/linux/usb.h` as follows:

```c
struct usb_device {
    /* ... */
    enum usb_device_state state;    /* Configured, Not Attached, etc */
    enum usb_device_speed speed;    /* High/full/low (or error) */
    /* ... */
    struct usb_device *parent;      /* Our hub, unless we're the root */
    /* ... */
    struct usb_device_descriptor descriptor; /* Descriptor */
    struct usb_host_config *config;         /* All of the configs */
    struct usb_host_config *actconfig;      /* The active config */
    /* ... */
    int maxchild;                       /* No: of ports if hub */
    struct usb_device *children[USB_MAXCHILDREN]; /* Child devices */
    /* ... */
};
```

We use this structure when we develop an example driver for a USB telemetry card later.

### USB Request Blocks

USB Request Block (URB) is the centerpiece of the USB data transfer mechanism. A URB is to the USB stack, what an `sk_buff` (discussed in Chapter 15, “Network Interface Cards”) is to the networking stack.

Let's take a peek inside a URB. The following definition is from `include/linux/usb.h`, omitting fields not of particular interest to device drivers:

```c
struct urb
{
    struct kref kref;           /* Reference count of the URB */
    /* ... */
    struct usb_device *dev;     /* (in) pointer to associated
                             device */
    unsigned int pipe;         /* (in) pipe information */
    int status;                 /* (return) non-ISO status */
    unsigned int transfer_flags; /* (in) URB_SHORT_NOT_OK | ... */
    void *transfer_buffer;      /* (in) associated data buffer */
    dma_addr_t transfer_dma;     /* (in) dma addr for
                             transfer_buffer */
    int transfer_buffer_length;  /* (in) data buffer length */
};
```

![](img/07cc6f9c8c74622020874f66bfb53dc4_292_0.png)
![](img/07cc6f9c8c74622020874f66bfb53dc4_293_0.png)
![](img/07cc6f9c8c74622020874f66bfb53dc4_297_0.png)
