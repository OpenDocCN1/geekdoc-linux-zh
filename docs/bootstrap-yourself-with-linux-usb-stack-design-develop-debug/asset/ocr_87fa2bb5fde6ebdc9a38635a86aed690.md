# Chapter 10 = Host Driver for Embedded Controller

+   - int usb_hcd_link_urb_to_ep(struct usb_hcd *hcd, struct urb *urb)

The HCD enqueue function calls this function to add a URB to the point queue. The function returns 0 on success and a negative value on failure indicating the reason for the failure.

+   - void usb_hcd_unlink_urb_from_ep(struct usb_hcd *hcd, struct urb *urb)
This interface function is called to remove a URB from an endpoint queue. The function returns 0 on success and a negative value on failure indicating the reason for the failure.

This section explored some of the essential data structures and interfaces required to implement a HCD. Check out the other definitions available at drivers/usb/core/hcd.h. The following section explores the HCD internals and the sequence of activity between the HCD and the usbcore.

# LINUX USB HCD

The Linux USB HCD is the lowermost part of the USB host framework that interacts with the USB host controller hardware. The USB host driver implements USB host specifications that the controller hardware supports. The Linux USB host driver is available in the drivers/usb/host/ folder. Its interface with the usbcore is through /drivers/usb/core/hcd.c.

Figure 10.1 illustrates a simple breakdown of the functions of an HCD.

The USB host consists of three major functionalities to make a complete framework: platform drivers, HCI, and HCD. The two former modules are interface functionalities for hardware and the usbcore module, respectively. The USB host controller hardware integrates with the platform hardware through glue logic. Glue logic is custom logic circuitry that interfaces integrated circuits. The hardware glues are supported through the platform driver routines. In a normal USB host system, interfaces such as PCI act as glue logic to interfaces. In an embedded system, the USB controllers are interfaced through a complex bus interface controller to GPIO and pins.

A USB HCD is developed for every USB host controller. To control the HCD from usbcore, the usbcore uses interface routines that invoke the necessary callbacks of the HCD. The main functionality of the HCD is to implement