SUBSYSTEM="net" - This tells Udev to ignore devices that are not network cards.

+   - ACTION="add" - This tells Udev to ignore this rule for a uvent that isn't an add ('remove' and 'change') events also, but don't need to rename interfaces.

+   - DRIVERS="*" - This exists so Udev will ignore VLAN or bridge sub-interfaces (because sub-interfaces do not have drivers). These sub-interfaces are skipped because the name that would be assigned would collide with the parent devices.

+   - ATTR{address} - The value of this key is the NIC's MAC address.

+   - ATTR{type="*" - This ensures the rule only matches the primary interface in the case of wireless devices, which create multiple interfaces. The secondary interfaces are skipped for the same reason that VLAN and bridge sub-interfaces are skipped: there would be a name collision otherwise.

+   - NAME - The value of this key is the name Udev will assign to this interface.

The value of NAME is the important part. Make sure you know which name has been assigned to your network cards before proceeding, and be sure to use NAME when generating your configuration files below.

# 74.2. CD-ROM symlinks

Some software that you may want to install (e.g., various media players) expect the /dev/cdrom and /dev/dvd symlinks to exist, and point to a CD-ROM or DVD-ROM device. Also, it may be convenient to refer to these symlinks into /etc/stab. Udev comes with a script that will generate rules to follow these symlinks for you, depending on the capabilities of each device, and you will need to decide which modes of operation you wish to have the script use.

The first can operate in "by-path" mode (used by default for USB and FireWire devices), where the rules depend on the physical path of the CD or DVD device. Second, it can in "by-id" mode (default for IDE and SCSI devices), where the rules depend on identification strings stored in the CD or DVD device itself. The path is determined by Udev's path_id script, and the identification strings are read from the hardware by its at_id or scsi_id programs, depending on which type of device you use.

There are advantages to each approach; the correct approach to use will depend on what kind of devices changes may happen. If you expect the physical path to the drive (that is, the ports and/slots that it plugs into) to change, for example you may plan on moving the drive to a different IDE port or a different USB connector, then you use the "by-id" mode. On the other hand, if you expect the device's identification to change, for example you may replace it with a different device with the same capabilities and which is plugged into the system connectors, then you use the "by-path" mode.

If either type is possible with your drive, choose a mode based on the type of device you expect to happen more often.

> Important
External devices (for example, a USB-connected CD drive) should not use by-path persistence, because each time the device is plugged into a new external port, its physical path will change. All-connected devices will have this problem if you write Udev rules to recognize by their physical path; the problem is not limited to CD and DVD drives.

If you wish to see the values that Udev scripts will use, for the appropriate CD-ROM device, the corresponding directory under /sys (e.g., this can be /sys/block/hdd) and run a command similar to the following:

```
udevadm test /sys/block/hdd
```