hwdown unbinds a device from it's driver, but does not unload the driver module automatically.

There are two different ways how hwup gets information about devices and about the driver that needs to be loaded for a device:

+   - From Configuration Files
+   - From sysfs

# From Configuration Files

When a device needs to be initialized, hwup first tries to read a device configuration from files in the directory
/etc/sysconfig/hardware/.

In order to determine the correct configuration file, the configuration filenames follow a specific naming scheme.

The following is the filename for a PCI network adapter:

```
hwcfg-bus-pci-0000:02:08.0
```

The filename consists of the keyword hwcfg and the hardware description of a device.