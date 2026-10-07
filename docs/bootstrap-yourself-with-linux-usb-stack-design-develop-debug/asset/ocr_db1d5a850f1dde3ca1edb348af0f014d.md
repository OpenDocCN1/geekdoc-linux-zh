# Chapter 7 = Power Management

The USB host framework also includes system power management, which is executed with a similar sequence of activities. In a system power management activity, the suspend operation powers down the host controllers using host controller driver power management operations along with the USB connected device. The major difference in suspending a host controller is that the management framework invokes hcd_bus_suspend instead of usb_port_suspend. To resume, the hcd_bus_resume is invoked instead of usb_port_resume. The hcd_bus_suspend and hcd_bus_resume internally invoke the host controller driver's bus_suspend(ex: ehci_bus_suspend) and bus_resume(ex: ehci_bus_resume) call-backs. These host controller power management frameworks are available as part of the host controller driver files in drivers/usb/host/*.

Having explored the runtime and system-level power management, the next section discusses the procedure to control USB devices using runtime power management with a practical session.

# SETTING Up LINUX-USB POWER MANAGEMENT

You can control the USB power management framework through the parameters exported by the uscore and through the sysfs file from the user space. The USB power management framework is part of the uscore module, and the autosuspend parameter is available in the following path.

```
root@rajaram-laptop:/sys/module/usb/parameters/# cat autosuspend
```

The autosuspend holds a default value of 2. The device goes to suspend mode after 2 seconds of idleness. You can modify the suspend time by updating the autosuspend parameter. When the autosuspend parameter is set with the value -1, the auto suspend operation is disabled.

There are other sets of files in the power directory of the USB device's sysfs directory /sys/bus/usb/devices. Linux 2.6.34 contains three main files to manage runtime power from user space: wakeup, level, and autosuspend.

+   - wakeup. This file indicates whether the device supports the remote wakeup mechanism. If this file is empty, the device does not support remote wakeup. Normally when the device supports remote wakeup the file contains enabled or disabled.