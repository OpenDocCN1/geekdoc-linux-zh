# USB Mode Driver Using libusb

# A Simple USB Test Application Using libusb

It’s not always necessary to use libusb for standard applications as lippptp or isusb. Because libusb is a generic driver, it allows you to develop device drivers for custom devices. A custom device, for example, could be a standalone USB chip that has no functionality available, doesn't fit into class drivers, and needs special drivers. Also, in a typical validation setup, USB transfer requirements could be different from the standard requests, perhaps to simulate and send a nonstandard size of bulk data to check whether the hardware can handle the transfer as per specification or to invalid control data to check whether the software stack handles the situation properly. You can easily meet such needs of a validation system using libusb instead of developing device drivers, which are more complicated.

The following example illustrates how to write a driver that bulk reads and writes to a USB device. Any libusb program has to start with a call to initialization routines. The libusb library requires three such calls so that the libusb application is ready as the driver.

```
usb_init();
usb_find_busses();
usb_find_devices();
```

These steps allow the libusb to read the system configuration and update it with device information. Once these steps have been performed successfully, the program must identify the device using the Vendor ID and Product ID and take control of the device. The following code illustrates a possible method to get a USB device handler.

```
usb_dev_handle *open_usb_device(unsigned int MY_VID, unsigned int MY_PID)
{
    struct usb_bus *bus;
    struct usb_device *dev;

    for (bus = usb_get_busses(); bus; bus = bus->next)
    {
        for (dev = bus->devices; dev; dev = dev->next)
        {
            if (dev->descriptor.idVendor == MY_VID
                && dev->descriptor.idProduct == MY_PID)
        }
    }
```