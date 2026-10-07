# USB Network Gadget

The USB-IF CDC specification also defines Ethernet emulation over USB through the Ethernet Control Model (ECM) class. This defines a communications interface to configure and manage various Ethernet functions. On Linux, drivers/usb/gadget/ether.c, drivers/usb/gadget/f_ecm.c, and drivers/usb/gadget/u_ether.c files implement ECM gadget functionality and the host. Figure 19.3 illustrates the Linux USB Ethernet module in simple blocks.

The USB Ethernet module g_ether module supports ECM (Ethernet Control), EEM (Ethernet Emulation Model), and NDIS (Network Driver Interface Specification) functionalities. You can manage the g_ether module by module parameters next.

+   * use_eem. This informs the module whether it should support EEM. By default, the value is false.
* host_addr. This parameter sets the host Ethernet address.
* dev_addr. This parameter sets the device Ethernet address.

![](bbox=[0.075, 0.57, 0.585, 0.825])

Figure 19.3 Linux USB Ethernet modules in simple blocks.