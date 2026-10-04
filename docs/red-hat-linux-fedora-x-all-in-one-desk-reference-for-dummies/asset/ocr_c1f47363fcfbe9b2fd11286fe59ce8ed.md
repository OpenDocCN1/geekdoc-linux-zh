# 14 What Is Fedora Core?

Internally, the 2.6 kernel raises many internal limits for number of users to the maximum number of open files. For example, number of unique users and groups has been increased from 65,536 to over 4 billion. The maximum number of open files can now grow as needed. File systems can be as large as 16TB (that's about 16,000 gigabytes!).

Linux 2.6 also increases the limits on the major and minor device numbers, which were used to a maximum of 255 in earlier kernels. These device numbers translate to 255 types and 255 devices of a single type. In kernel version 2.6, the major device numbers can be up to 4,095 and minor device numbers can be more than a million. The upshot is that Linux 2.6 can support more device types and many devices of a single type.

# Improved device handling

Linux 2.6 has many of new features for handling devices — especially hot plug devices such as the ones that connect to USB and Firewire interfaces common in today's PCs. First, the kernel uses a virtual file system called sysfs which is meant to hold information about the devices on the system. The sysfs file system mounts /sys and it presents a hierarchical view of all the devices by device type, bus, and so on. Through sysfs, the 2.6 kernel makes available to other applications a lot of information about devices, including the name of a device, resources such as interrupts and I/O ports used by the device, the power status of device, and so on.

By using sysfs capabilities available in the 2.6 kernel, a separate device handling program called udev can now dynamically add devices when a device is added to a system. The udev program is invoked by the /sbin/hotplug script that runs when any hot plug device is plugged into the computer. udev gives each device a name that stays the same time device connects to the system. In Fedora Core, udev is not configured by default to manage the device files in /dev directory. Instead udev manages device files in the /udev directory. However, you can easily configure udev (through the /etc/udev/conf file) to manage the device files in /udev directory.

Other device handling improvements in Linux 2.6 include ensuring that device drivers are not unloaded while still in standardization the way in which device drivers make available information about devices they support. — kernel object — instead of the generic .o extension used for object files.

Linux 2.6 also has improved support for many devices such as USB 2.0 and wireless devices. As storage devices, the Integrated Drive Electronics (IDE) — also called AT Attachment (ATA) — Small Computer System Interface (SCSI) support was updated in Linux 2.6. For example, IDE