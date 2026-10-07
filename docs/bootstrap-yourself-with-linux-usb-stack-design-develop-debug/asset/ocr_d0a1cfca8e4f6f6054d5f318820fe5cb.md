# Chapter 16 ■ USB Virtual Systems

![](bbox=[0.082, 0.093, 0.917, 0.545])

Figure 16.4
Kernel configuration option to enable gadgetfs.

configure the device through Endpoint Zero. The other set of files, named /dev/
gadget/ep*, is created for each endpoint under the driver binding, which allows
you to communicate respective endpoints.

The /dev/gadget/$SHIP file allows you to open Endpoint Zero and write
descriptors for the gadget framework. This enables the kernel to bind to the
USB controller and reads it for enumeration.

```
fd = open("/dev/gadget/$SHIP", 0_RDWR)
status = write(fd, sizeof descriptors)
```

The device is active and ready for enumeration until you close the file descriptor.
You can obtain the events in the next table when you poll the file and read the
status of the gadget framework.