| Objective | Summary |
|---|---|
| 5. Describe the sysfs File System | The sysfs file system provides a representation of all devices and interfaces of a system.

Devices are represented in the directories: /sys/bus and /sys/devices.

Interfaces are represented by the directories /sys/class and /sys/block.

A device and its interfaces are connected with file system links. |
| 6. Describe how udev Works | In SUSE Linux Enterprise Server 10, udev also replaces the hotplug system, which was responsible for the initialization of hardware devices in previous versions. udev is the central point for hardware initialization in SUSE Linux Enterprise Server 10. |
| 7. Use the hwup Command | hwup is used to load device drivers. Information about the required drivers for a device is either taken from a configuration file under /etc/sysconfig/hardware/ or from the file /lib/modules/kernel_version/modules.aliases. |