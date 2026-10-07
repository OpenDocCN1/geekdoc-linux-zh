# Bootstrap Essentials: Platform Driver

Generally, the struct platform_device is installed as part of module initialization and registered onto the platform driver framework. The platform driver framework passes the struct platform_device object with the resource allocated to the driver using the probe method, where the resources are remapped to the device driver data structures.

The next key data structure is the struct platform_driver. It is similar to the standard Linux driver model, which provides methods to identify and manage the device. You have to register handler routines to the device to handle calls from the platform driver framework. Of these handler routines, the probe and the remove methods are specific for a device driver to be functional.

```
struct platform_driver {
int (*probe)(struct platform_device*);
int (*remove)(struct platform_device*);
void (*shutdown)(struct platform_device*);
int (*suspend)(struct platform_device*, pm_message_t state);
int (*resume)(struct platform_device*);
struct device_driver driver;
};
```

After successful initialization of the struct platform_driver with methods specific to the device, you need to register the methods with the platform driver framework. You use the platform_driver_register method to register the struct platform_driver_register methods to the platform driver framework.

```
int platform_driver_register(struct platform_driver *);
```

When the hardware is not pluggable and needs detection during booting the kernel, you must use the platform_driver_probe method. This method is ideal for platform drivers, which are for controllers integrated with the platform hardware. This method works similarly to the platform_driver_register, except hardware is not probed when another device is connected after the kernel boot.

```
int platform_driver_probe(struct platform_driver *driver, int (*probe)(struct platform_device *));
```

# Note

+   Using the platform_driver_probe method reduces the runtime memory footprint. Also, the driver isn't probed if another device is registered.