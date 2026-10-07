# CHAPTER 8

# Hub

In This Chapter

+   - Bootstrap Essentials: Linux USB Hub
- Linux USB Hub Framework

The universal serial bus (USB) standard supports up to 127 physical device connections by a host. But a typical host computer supports a limited number of ports and thus can connect only a few devices. The USB specification defines a device model referred to as a *hub device* that allows a host to extend its port and connect multiple devices. A USB hub controller is integrated with a root hub to provide one or more attachment points. Figure 8.1 illustrates a typical, root hub, hub, and device relationship.

The Linux USB framework supports a USB hub as part of the `usb` module and provides a virtual root hub framework for host controllers. The Linux hub framework provides functionalities required by Chapter 11, “USB Specification,” of the USB 2.0 specification, such as hub event and change requests. The framework also plays a role in the enumeration process, as well as setting the address, connection/disconnection, and reset, as well as in On-the-Go (OTG) functionality and power management of the Linux USB hub functionality.

The next sections explore essential data structures required for the Linux USB hub framework. That’s followed by the functionalities and activity sequence of the hub framework with other Linux USB host framework subsystems.