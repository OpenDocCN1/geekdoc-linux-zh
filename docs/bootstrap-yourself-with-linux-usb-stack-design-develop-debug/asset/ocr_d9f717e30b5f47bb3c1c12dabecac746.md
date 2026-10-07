# Chapter 6 = Device File System

During initialization, the framework registers with the USB notification to get events when new USB bus and USB devices are added to the system. The usbfs_nb notifier block defined as /drivers/usb/core/inode.c registers the usbfs_notify callback handler to collect addition and removal events from the USB bus/device.

```
static struct notifier_block usbfs_nb = {
    notifier_call = usbfs_notify,
};
static int usbfs_notify(struct notifier_block *self, unsigned long action, void *dev)
{
    switch (action) {
        case USB_DEVICE_ADD:
            usbfs_add_device(dev);
            break;
        case USB_DEVICE_REMOVE:
            usbfs_remove_device(dev);
            break;
        case USB_BUS_ADD:
            usbfs_add_bus(dev);
            break;
        case USB_BUS_REMOVE:
            usbfs_remove_bus(dev);
            break;
    }
    usbfs_update_special();
    usbfs_conn_disc_event();
    return NOTIFY_OK;
}
```

The usbfs_notify receives four events that indicate the addition and removal of USB devices and USB bus. These events trigger the creation of USB files by setting up the VFS objects within the framework.

Figure 6.3 illustrates the sequence of activities during initialization and exit of the USB VFS framework. The USB VFS framework starts when the uscore calls upon the usbfs_init function registers to the USB file system and notifier callback. The registration to the file system triggers creation of the super block objects. Similarly, during exit of the module uscore, the usbfs_cleanup function is called, which successfully unregisters the file system and the notifier callback.