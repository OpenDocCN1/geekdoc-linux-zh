# **127**

Chapter 5. Character Drivers

```
```
printk("LED Driver Initialized.\n");
    return 0;
}

/* Driver Exit */
void __exit
led_cleanup(void)
{
    unregister_chrdev_region(MAJOR(dev_number), 1);
    class_device_destroy(led_class, MKDEV(MAJOR(dev_number), 0));
    class_destroy(led_class);
    return;
}

module_init(led_init);
module_exit(led_cleanup);

MODULE_LICENSE("GPL");
```
```

`led_init()` is similar to `cmos_init()` developed in Listing 5.1, but for a couple of things:

+   1.  As you saw in Chapter 4, the new device model distinguishes between drivers and devices. `led_init()` registers the LED driver with parport via a call to `parport_register_driver()`. When the kernel finds the LED board during `led_attach()`, it registers the device by invoking `parport_register_device()`.
+   2.  `led_init()` creates the device node `/dev/led`, which you can use to control the state of individual LEDs.

Compile and insert the driver module into the kernel:

```
```bash
bash> make -C /path/to/kernel/tree M=$PWD modules
bash> insmod ./led.ko
LED Driver Initialized
```
```

To selectively drive some parallel port pins and glow the corresponding LEDs, echo the appropriate value to `/dev/led`:

```
```bash
bash> echo 1 > /dev/led
```
```

Because ASCII for 1 is 31 (or `00110001`), the first, fifth, and sixth LEDs should turn on.

The preceding command triggers invocation of `led_write()`. This driver method first copies user memory (the value 31 in this case) to kernel buffers via `copy_from_user()`. It then claims the parallel port, writes data, and releases the port, all using parport interfaces.

Sysfs is a better place than `/dev` to control device state, so it's a good idea to entrust LED control to sysfs files. Listing 5.7 contains the driver implementation that achieves this. The sysfs manipulation code in the listing can