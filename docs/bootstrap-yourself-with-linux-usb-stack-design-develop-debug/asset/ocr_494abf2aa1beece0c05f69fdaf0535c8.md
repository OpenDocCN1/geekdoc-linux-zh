# Chapter 3 = Overview of the Linux USB Subsystem

# Table 3.1 Linux USB Framework Directory Structure

| Folder Name | Description |
| --- | --- |
| Core | Part of the Linux USB host framework contains sources implementing the USB software system, including the hub, the USB file system, and the USB protocol implementation of the host. |
| Host | Part of the Linux USB host framework contains the controller drivers. This source code includes EHCI¹, UHCI², and OHCI³ drivers for embedded USB host controllers. |
| Gadget | Contains source code that implements USB peripheral framework and drivers for the USB peripheral framework. The USB device part of class implementation and the related framework are also available in this folder. |
| Otg | Contains source code that implements OTG⁴ driver framework and drivers for OTG controllers. |
| Class | Contains source code that implements a USB class protocol as ACM⁵ for the USB host and others that don't fall under any of the categories that follow. |
| Storage | Contains source code that implements a USB storage driver for a USB host, which includes support to different memory types. |
| Image | Contains source code implements drivers for imaging devices such as cameras or scanners for the USB host. |
| Atm | Contains sources that implement drivers for modern modems for the USB host. |
| Serial | Contains source code implements drivers for serial devices such as serial consoles or adapters for the USB host. |
| Misc | Contains source code that implements drivers for the USB host that do not fall into this category, such as the USB test drivers. |

> ¹EHCI = Enhanced Host Controller Interface
²UHCI = Universal Host Controller Interface
³OHCI = Open Host Controller Interface
⁴OTG = On-the-Go
⁵ACM = Abstract Control Interface

You can download the Linux kernel source 2.6.34 from http://www.kernel.org/. The Linux USB framework is organized under the *drivers/usb* folder of the Linux kernel source package. The *drivers/usb* folder contains source of the USB framework, which can handle both USB device and host functionalities. Table 3.1 is an overview of the directory structure of the Linux USB framework.