# Overview of Linux USB Stack Architecture

implements the necessary infrastructure for transfer of data between the client application and the HCD.

# HCD

The HCD implements the driver for Enhanced Host Controller Interface (EHCI), Open Host Controller Interface (OHCI), and other custom USB host controllers. It also provides the necessary abstraction to the hardware below. In general, the HCDs are based on the type of interface they use to connect to the main processor. On a personal computer, the host controllers primarily interface using Peripheral Component Interconnect (PCI); therefore, the HCDs are based on the PCI framework. On an embedded system, the interfaces vary, depending on the system requirement and the interface availability.

# OVERVIEW OF LINUX USB HOST STACK ARCHITECTURE

The Linux host stack consists of two major parts: the usbcore available in the /drivers/usb/core folder and the HCDs available in /drivers/usb/host/. The usbcore module implements both the host software and the USBD functionalities. Figure 4.2 represents the Linux USB host stack in a simple way.

# usbcore

The USB system software module is named usbcore and consists of the following modules: device management, power management, USB hub driver, USB host driver, and HCD interfaces.

# Device Management

As part of device management, the Linux USB subsystem implements functionalities that help manage USB devices connected to the host. The USB devices that are connected to the host share information via virtual file systems (VFS) of Linux as part of the sysfs and profs systems. The devices also implement frameworks such as device notification, allowing the host system to report the addition or removal of devices to other modules.

# Power Management

The USB specification defines methods to save power on USB devices and is implemented as part of the usbcore. The power management framework on