# list_devices

The device and all device special files associated with the device are listed. The device argument is optional, and if it is not present, all relevant devices are listed.

# Options

+   - -1 [device]
List the path name(s) of the device special files associated with the device that are allocatable to the current process. If device is given, list only the files associated with the specified device.

+   - -n [device]
List the path name(s) of device special files associated with the device that are allocatable to the current process but are not currently allocated. If you specify device, list_devices lists only the files associated with that device.

+   - -s
Silent. Suppress any diagnostic output.

+   - -u [device]
List the path name(s) of device files associated with the owner of the current process. If you specify device,list_devices lists only the files associated with that device.

+   -U uid
Use the user ID of the real user ID of the current process when performing the list_devices operation. Only a user with solaris.devices.revoke authorization can use this option.

# Examples

```
The following example shows the long listing for list_devices command.
mopoke@ list_devices -1
device: audio type: audio files; /dev/audio /dev/audioctl1 /dev/sound/
dev/sound/octl
device: fd0 type: fd files; /dev/diskette /dev/rdiskette /dev/fd0a
dev/rdf0a /dev/fd0 /dev/fd0b /dev/rdf0b /dev/fd0c /dev/fd0d
dev/rdfd0
device: sr0 type: sr files; /dev/sr0 /dev/disk/clt1d00
dev/disk/clt1d01 /dev/disk/clt1d02 /dev/disk/clt1d03
dev/disk/clt1d04 /dev/disk/clt1d05 /dev/disk/clt1d06
dev/disk/clt1d07 /dev/rdsk/clt1d00 /dev/rdsk/clt1d01
dev/rdsk/clt1d02 /dev/rdsk/clt1d03 /dev/rdsk/clt1d04
dev/rdsk/clt1d05 /dev/rdsk/clt1d06 /dev/rdsk/clt1d07
mopoke@
```

# Diagnostics

list_devices returns a non-zero exit status in the event of an error.

# Files

```
/etc/security/device_allocate
```

Mandatory access control information about each device.