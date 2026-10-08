# allocate 39

information from the device or driver internal storage after another user is finished with the device.

For example, several users share a single tape drive that may not be located at an individual user's location. If the tape drive is located remotely, some time can elapse between the time the user loads a tape in the drive and the user invokes a command to access the tape drive. Because other users could access the drive while the tape is unattended, another user could access or overwrite the data on the tape. With the device allocation mechanism, you can ensure that one user at a time has access to a specific tape device.

To preserve the integrity of the device, the allocate operation is executed on all the device special files associated with that device.

Only authorized users can allocate a device. The required authorizations are specified in device_allocate(4).

# Options

+   -g dev-type

Allocate a nonallocated device with a device type matching dev-type. Use the dev-type argument to specify the type of device. You can determine the type of device from the output of the list_devices -1 command. See "Examples" for an example.

+   -s

Suppress diagnostic output.

+   -F device

Reallocate a device to another user. This option is often used with -U to reallocate a specific device to a specific user. Only a user with the solaris.devices.revoke authorization is permitted to use this option.

Use the device argument to specify the device to be manipulated, example st0 for a streaming tape device. You can display a list of available devices with the -1 option to the list_devices(1) command, also new in the Solaris 9 Operating Environment. See "Examples" on page 685 for an example of the output from list_devices -1. The default allocation operation allocates the device special files associated with the UID of the current process.

When you specify the -F option, the device-cleaning program is executed when performed. In /etc/security/lib. The name of this program is found in the device_allocate(4) entry for the device in the dev-exec-fd.

+   -U uname

Use the user ID uname instead of the user ID of the current process when performing allocate operation. Only a user with the solaris.devices.revoke authorization is permitted to use this option.

# Examples

The following example allocates a tape drive.

```
mokoke% allocate st0
mokoke%
```