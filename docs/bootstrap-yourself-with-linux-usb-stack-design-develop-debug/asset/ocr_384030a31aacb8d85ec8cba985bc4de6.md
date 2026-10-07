# Chapter 2 = USB: An Overview

system software to take appropriate action. The host controller ensures USB protocol rules for bus management, such as interpacket timings and timeouts.
Now you've read a brief overview of the USB host's internal blocks, the following sections focus on the internal details of a USB device system.

# USB Device

A USB device to an end user provides additional capability, such as Web camera or printer, to a host computer through a USB interface. In fact, a USB hub is referred to as a device that provides additional USB attachment points to a host computer. A USB device is generally self-powered or bus powered (powered by the USB host). Figure 2.5, taken from the USB specification, is a simplified version of Figure 2.3 illustrating the blocks of USB device. The subsequent section provides an overview of these USB device layers.

# Function

The function layer implements the functional characteristic of the USB device. This layer implements the USB class specifications such as mass storage, HID, and communication defined by USB.org. In Figure 2.3, notice that the USB

![](bbox=[0.085, 0.558, 0.423, 0.856])

Figure 2.5
USB device layers and information flow.