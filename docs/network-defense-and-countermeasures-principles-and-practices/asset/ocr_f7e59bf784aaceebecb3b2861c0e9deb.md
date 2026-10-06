# netstat

The netstat command is also used to detect ongoing attacks. It lists all current network connections, not just inbound, but outbound as well. You can see this utility in Figure 16-7.

![](bbox=[0.071, 0.197, 0.636, 0.453])

# The Windows Registry

The Windows Registry is an incredible repository of potential valuable forensics information. It is the heart of the Windows machine. You can find a number of interesting pieces of data here. It is beyond the scope of this chapter to make you an expert in the Windows Registry, but it is hoped that you will continue and learn more. One important thing you can find, from a forensics perspective, is any USB devices that have been connected to the machine.

The registry key HKEY_LOCAL_MACHINE\SYSTEM\ControlSet\Enum\USBSTOR lists USB devices that have been connected to the machine. It is often the case that a criminal will move evidence to an external device and take it with them. This could indicate that there are devices you need to find and examine.

# USB Information

There are other keys related to USBSTOR that provide related information. For example, SYSTEMMountedDevices allows investigators to match the serial number to a given drive letter or volume that was mounted when the USB device was inserted. This information should be combined with the information from USBSTOR in order to get a more complete picture of USB-related activities.

The registry key SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2 will indicate what user was logged onto the system when the USB device was connected. This allows the investigator to associate a specific user with a particular USB device.