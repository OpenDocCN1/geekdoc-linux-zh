# The Linux Device Model

The new Linux device model introduces C++-like abstractions that factor out commonalities from device drivers into bus and core layers. Let’s look at the different components constituting the device model such as *udev*, *sysfs*, *kobjects*, and *device classes* and their effects on key kernel subsystems such as /dev node management, hotplug, firmware download, and module autoload. *Udev* is the best vantage point to view the benefits of the device model, so let’s start from there.

# Udev

Years ago when Linux was young, it was not fun to administer device nodes. All the needed nodes (which could run into thousands) had to be statically created under the /dev directory. This problem, in fact, dated all the way back to original UNIX systems. With the advent of the 2.4 kernels came *devfs*, which introduced dynamic device node creation. *Devfs* provided services to generate device nodes in an in-memory filesystem, but the onus of naming the nodes still rested with device drivers. Device naming policy is administrative and does not mix well with the kernel, however. The place for policy is in header files, kernel module parameters, or user space. *Udev* arrived on the scene to push device management to user space.

*Udev* depends on the following to do its work:

+   1. Kernel *sysfs* support, which is an important part of the Linux device model. *Sysfs* is an in-memory filesystem mounted under /sys at boot time (look at /etc/fstab for the specifier). We will look at *sysfs* in the next section, but for now, take the corresponding *sysfs* file accesses for granted.
+   2. A set of user-space daemons and utilities such as *udevd* and *udevinfo*.
+   3. User-specified rules located in the /etc/udev/rules.d/ directory. You may frame rules to get a consistent view of your devices.

To understand how to use *udev*, let’s look at an example. Assume that you have a USB DVD drive and a USB CD-RW drive. Depending on the order in which you hotplug these devices, one of them is assigned the name /dev/sr0, and the other gets the name /dev/sr1. During pre-*udev* days, you had to figure out the associated names before you could use the devices. But with *udev*, you can consistently view the DVD (as say, /dev/usbdvd) and the CD-RW (as say, /dev/usbcdmw) irrespective of the order in which they are plugged in or out.

First, pull product attributes from corresponding files in *sysfs*. Assume that the (Targus) DVD drive has been assigned the device node /dev/sr0 and that the (Addonics) CD-RW drive has been given to the name /dev/sr1. Use *udevinfo* to collect device information:

Code View:

```
```
bash> udevinfo -a -p /sys/block/sr0
...
  looking at the device chain at
  `/sys/devices/pci0000:00/0000:00:1d.7/usb1/1-4':
  BUS==`usb`
  ID==`1-4`
  SYSFS{bConfigurationValue}==`1`
...
```
```