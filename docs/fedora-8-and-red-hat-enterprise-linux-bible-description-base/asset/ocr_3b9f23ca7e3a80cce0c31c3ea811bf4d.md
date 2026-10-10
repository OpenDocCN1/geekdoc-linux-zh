You can use the `-d` option to list just the description, the `-a` option to see the author of the module or `-n` to see the object file representing the module. The author information often has the e-mail address of the driver's creator, so you can contact the author if you have problems or questions about it.

# Loading modules

You can load any module that has been compiled and installed (to the /lib/modules directory) into your running kernel using the modprobe command. The most common reasons for loading a module are that you want to use a feature temporarily (such as loading a module to support a special file system on a floppy you want to access) or to identify a module that will be used by a particular piece of hardware that could not be autodetected.

Here is an example of the modprobe command being used to load the parport module. The parport module provides the core functions to share parallel ports with multiple devices.

```
# modprobe parport
```

After parport is loaded you can load the parport_pc module to define the PC-style ports available through the interface. The parport_pc module lets you optionally define the addresses and IRQ numbers associated with each device sharing the parallel port. For example:

```
# modprobe parport_pc io=0x3bc irq=auto
```

In the previous example, a device is identified as having an address of 0x3bc. The IRQ for the device is autodetected.

The modprobe command loads modules temporarily. At the next system reboot, the modules you enter disappear. To permanently add the module to your system, add the modprobe command line to one of the start-up scripts that are run a boot time.

> **NOTE:** An alternative to using modprobe is the insmod command. The advantage of using modprobe, however, is that insmod will only load the module you request, while modprobe will try to load other modules that the one you requested is dependent on.

# Removing modules

You can remove a module from a running kernel using the rmmod command. For example, to remove the module parport_pc from the current kernel, type the following:

```
# rmmod parport_pc
```

If the module is not currently busy, the parport_pc module is removed from the running kernel. (Instead of rmmod, you can use modprobe -r to remove the module, plus related modules.)