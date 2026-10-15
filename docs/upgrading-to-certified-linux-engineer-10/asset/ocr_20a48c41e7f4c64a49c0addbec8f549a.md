| Objective | Summary |
|---|---|
| 2. Describe how Device Drivers Work (continued) | - **rmmod**. Use rmmod to remove loaded kernel modules.

The kernel modules are files that are stored in the directory `/lib/modules/kernel-version/`. |
| 3. Describe how Device Drivers Are Loaded | In a SUSE Linux Enterprise Server 10 system, kernel modules are loaded in the following ways:

- From initrd
- By initscripts
- By udev
- By the X Server
- Manually by the user root |
| 4. Manage Kernel Modules Manually | The hwup command is used to start preconfigured devices.

The device configuration files are stored in the directory `/etc/sysconfig/hardware/`.

The filename of the configuration file contains a unique identifier for the corresponding device.

In the configuration file, the following variables can be used:

- STARTMODE
- MODULE
- MODULE_OPTIONS
- SCRIPT{UP,DOWN}[type]
- SCRIPT{UP,DOWN} |