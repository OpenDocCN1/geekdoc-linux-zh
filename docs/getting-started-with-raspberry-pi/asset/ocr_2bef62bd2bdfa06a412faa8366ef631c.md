MP3 player used in Chapter 13 , “Audio Drivers,” and the Bluetooth pill dispenser used in Chapter 16 are also examples of devices that can use the Linux cell phone to get Internet-enabled.

Listing 6.1 implements the `USB_UART` driver. It’s implemented as a *platform driver*. A platform is a pseudo bus usually used to tie lightweight devices integrated into SoCs, with the Linux device model. A platform consists of

+   1. A platform device. The architecture-specific setup code adds the platform device using `platform_device_register()` or its simpler version, `platform_device_register_simple()`. You may also register multiple platform devices at one shot using `platforms_add_devices()`. The `platform_device` structure defined in `include/linux/platform_device.h` represents a platform device:

```
```c
struct platform_device {
  const char *name;  /* Device Name */
  u32 id;            /* Use this field to register multiple
                     * instances of a platform device. In
                     * this example, the two USB_UARTs
                     * have different IDs. */
  struct device dev; /* Contains a release() method and
                     * platform data */
  /* ... */
};
```
```

+   2. A platform driver. The platform driver registers itself into the platform using `platform_driver_register()`. The `platform_driver` structure, also defined in `include/linux/platform_device.h`, represents a platform driver:

```
```c
struct platform_driver {
  int (*probe)(struct platform_device *); /*Probe method*/
  int (*remove)(struct platform_device *); /*Remove method*/
  /* ... */
  /* The name field in the following structure should match
     the name field in the associated platform_device
     structure */
  struct device_driver driver;
};
```
```

See `Documentation/driver-model/platform.txt` for more on platform devices and drivers. For simplicity, our sample driver registers both the platform device and the platform driver.

During initialization, the `USB_UART` driver first registers itself with the serial core using `uart_register_driver()`. When that is done, you will find a new line starting with `usb_uart` in `/proc/tty/drivers`. Next, the driver registers two platform devices (one per `USB_UART`) using `platform_device_register_simple()`. As mentioned earlier, platform device registrations are usually done during boot-time board setup. Following this, the driver registers platform driver entry points (`probe()`, `remove()`, `suspend()`, and `resume()`) using `platform_driver_register()`. The `USB_UART` platform driver ties into both the above platform devices and has a matching name (`usb_uart`). After this step, you will see two new directories appearing in sysfs, each corresponding to a `USB_UART` port: `/sys/devices/platform/usb_uart.0` and `/sys/devices/platform/usb_uart.1/`.

Because the Linux device layer now detects a platform driver matching the name of the registered `USB_UART` platform devices, it invokes the `probe()` entry point¹¹ (`usb_uart_probe()`) belonging to the platform driver, once for each `USB_UART`. The probe entry point adds the associated `USB_UART` port using `uart_add_one_port()`