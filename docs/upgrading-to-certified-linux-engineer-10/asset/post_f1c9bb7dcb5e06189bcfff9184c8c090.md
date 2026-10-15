
## Objective 2 Describe how Device Drivers Work

As described before, device drivers access and use a device. There are 2 basic kinds of device drivers:

- Kernel modules. The functionality of the Linux kernel can be extended by kernel modules. These modules can be loaded and removed during runtime. They allow the kernel to provide access to hardware.
- User space drivers. Some hardware needs additional drivers that work in user space. Examples of this kind of hardware are printers or scanners.

The following illustrates the roles of kernel and user space drivers:

![](img/8279afe915b153902294b0e58311b75a_48_0.png)

While the handling of user space drivers depends on the framework they are used in, you can manage kernel modules with the following commands:

- **lsmod.** This command lists all loaded kernel modules. For example:
  `lsmod`
- **modprobe.** This command loads kernel modules. Because kernel modules can depend on each other, modprobe automatically resolves these dependencies and loads all required modules. For example:
  `modprobe usb-storage`
  In this example, modprobe loads the usb-storage module which is needed to access storage devices connected with the USB bus.
  Because this module requires other USB modules, modprobe also loads these modules.
- **rmmod.** This command removes loaded kernel modules. For example:
  `rmmod usb-storage`
  Only modules that are not needed can be removed. In this example, the USB device first has to be disconnected before the usb-storage module can be removed.

Kernel modules are files that are stored in the directory `/lib/modules/kernel-version/`.

Modules are stored in several subdirectories with a filename extension of .ko for kernel object. When loading a module with modprobe, you can leave out the extension and use just the module name.

## Objective 3 Describe how Device Drivers Are Loaded

Because it would be very inconvenient to load all kernel modules manually after every system start, there are several methods to perform this task automatically.

The following is an overview of how device drivers are loaded in SUSE Linux Enterprise Server 10:

- **initrd.** Important device drivers that are necessary to access the root partition are loaded from initrd. initrd is a special file that is loaded into memory by the boot loader. Examples of such modules are the SCSI host controller and file system drivers.
- **initscripts.** Some initscripts are dedicated to loading and setting up hardware devices, such as the ALSA sound script for sound cards.
- **udev.** udev also loads kernel modules with the hwup command.
- **X Server.** Although the graphics card drivers are not kernel modules, X Server loads special drivers to enable hardware 3D support.
- **manually.** You can always load kernel modules on the command line or in scripts with the modprobe command or with the hwup or hwdown commands.

## Objective 4 Manage Kernel Modules Manually

Although SUSE Linux Enterprise Server 10 initializes most hardware devices automatically, it can be very helpful to know how kernel modules are managed manually.

To manage kernel modules, you need to understand the following:

- Kernel Module Basics
- Manage Modules from the Command Line
- modprobe Configuration File (/etc/modprobe.conf)

For the latest kernel documentation, see /usr/src/linux/Documentation.

## Kernel Module Basics

The kernel that is installed in the directory /boot/ is configured for a wide range of hardware. It is not necessary to compile a custom kernel, unless you want to test experimental features and drivers.

Drivers and features of the Linux kernel can either be compiled into the kernel or be loaded as kernel modules. These modules can be loaded later, while the system is running, without having to reboot the computer.

This is especially true of kernel modules that are not required to boot the system. By loading them as components after the system boots, the kernel can be kept relatively small.

The kernel modules are located in the directory /lib/modules/version/kernel/.

For example, the modules for the 2.6 kernel can be found in the following directory:

```
/lib/modules/2.6.16-0.12-default/kernel/
```
