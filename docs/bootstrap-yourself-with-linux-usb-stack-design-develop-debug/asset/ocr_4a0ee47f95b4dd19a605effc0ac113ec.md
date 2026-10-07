# Chapter 17 ■ User Space USB Drivers

![](bbox=[0.105, 0.098, 0.453, 0.216])

**Figure 17.1**
Different VFS programming options for USB user mode drivers.


programs can adopt to interact with a USB device from the user space. The usbfs, sys, and /dev files are part of the Linux-USB framework, where one part of the USB functionality lies inside the kernel drivers and a remaining part is controllable at the user level. The previous chapter detailed communication through normal file operations and through input/output controls (IOCTLs). This chapter starts with an overview of the Linux-USB host user space drivers and then covers how to develop USB user space drivers using usbfs and /sys with a USB device.

Linux also has generic frameworks to interact with devices from the user space, such as the user space IO (UIO), which provides a framework to write drivers in the user space. A minimal kernel driver using the UIO framework is developed to map the necessary hardware features to the user space. In the case of USB, you can adopt this generic method to develop a simpler validation system of USB controller hardware. Later, this chapter includes a quick boot-strap session on the UIO subsystem, explores how to program USB controller hardware based on the UIO subsystem, and writes a simple validation program using UIO for a USB device controller.

The chapter also covers the Linux-USB gadget framework user space program using the gadgetfs file system to interface with a USB gadget framework.

# OVERVIEW: USB USER MODE DRIVERS

Linux allows control of the physical devices from the user space through the VFS. The user space drivers are developed based on such virtual files. The USB framework provides virtual file usbfs to interact with the USB devices connected to the system. Also, remember with usbfs that the device driver is partly implemented in the kernel and partly at the user space.