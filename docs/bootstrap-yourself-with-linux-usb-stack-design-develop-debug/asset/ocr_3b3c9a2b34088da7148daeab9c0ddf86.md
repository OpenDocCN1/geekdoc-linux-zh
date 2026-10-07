# Chapter 2 = USB: An Overview

and the USB device. These layers establish a logical connection between these layers across the host through the pipes at the functional level and the endpoint at the lower layers. Also, notice that the device and bus interface layers work on USB-specific data, and the upper functional layer is specific to the class that the device implements. The following sections go into more detail about these layers for the host and the device, followed by the enumeration process and the USB transfer types.

# USB Host

The USB protocol is driven. The host is made up of three major layers: client software, USB system software, and USB host controller, which is the USB bus interface of the USB host. These layers are responsible for the complete USB system operation as a host, which includes detection and removal of device attachment, and data flow management with the device, and control of status and control of the electrical interface. Figure 2.4, taken from the USB specification, is a simplified version of Figure 2.3, illustrating the blocks of the USB host.

# Client Software

The client software refers to the software applications that interact with the USB devices using their functional aspect. For example, perhaps you connect a USB camera to your personal computer. The application that streams video is the client software for the USB Web camera. Thus, this layer interacts with the USB peripheral via the USB system software’s exposed interfaces in a level above the USB protocol. Generally, these software layers are unaware of USB activity other than identifying and opening USB devices.

# USB System Software

The USB system software is the core of the USB host system, performing most of the USB host activities. The USB system software is implemented over the host controller hardware and acts as an interface between the client software and the host controller. The system software consists of two major blocks: the host controller driver (HCD) and the USB driver (USBD). The HCD acts like a hardware abstraction layer, extending the USB host controller’s feature in a transparent way. Thus, the HCD layer allows the USBD to support different host