
files in `/sys/class/pardevice/led/control/`*
kobj.ktype = &ktype_led;

/* Register the kobject */
kobject_register(&kobj);

printk("LED Driver Initialized.\n");
return 0;
}

/* Driver Exit */
void
led_cleanup(void)
{
    /* Unregister kobject corresponding to
        /sys/class/pardevice/led/control */
    kobject_unregister(&kobj);

    /* Destroy class device corresponding to
        /sys/class/pardevice/led/ */
    class_device_destroy(led_class, MKDEV(MAJOR(dev_number), 0));

    /* Destroy /sys/class/pardevice */
    class_destroy(led_class);

    return;
}

module_init(led_init);
module_exit(led_cleanup);

MODULE_LICENSE("GPL");

The macro definition of *glow_show_led()* in Listing 5.7 uses a technique popular in kernel source files to compactly define several similar functions. The definition produces *read()* and *write()* methods (called *show()* and *store()* in sysfs terminology) attached to eight /sys files, one per LED on the board. Thus, *glow_show_led(0)* attaches *glow_led_0()* and *show_led_0()* to the /sys file corresponding to the first LED. These functions are respectively responsible for glowing/extinguishing the first LED and reading its status. ## glues a value to a string, so glow_led_##number translates to glow_led_0() when the compiler processes the statement, glow_show_led(0).

This sysfs-aware version of the driver uses a kobject to represent a “control” abstraction, which emulates a software knob to control the LEDs. Each kobject is represented by a directory name in sysfs, so *kobject_register()* in Listing 5.7 results in the creation of the /sys/class/pardevice/led/control/ directory.

A ktype describes a kobject. The “control” kobject is described via the *ktype_led* structure, which contains a pointer to the attribute array, *led_attrs[]*. This array contains the addresses of the device attributes of each LED. The attributes of each LED are tied together by the statement:

```
static struct led_attr led##number =
__ATTR(led##number, 0644, show_led_##number, glow_led_##number);
```

This results in instantiating the control file for each LED, /sys/class/pardevice/led/control/ledX, where X is the LED number. To change the state of ledX, echo a 1 (or a 0) to the corresponding control file. To glow the first LED on the board, do this:

```
bash> echo 1 > /sys/class/pardevice/led/control/led0
```

During module exit, the driver unregisters the kobjects and classes using kobject_unregister(), class_device_destroy(), and class_destroy().

Listing 7.2 in Chapter 7, "Input Drivers," uses another route to create files in sysfs.

Writing a char driver is no longer as simple as it used to be in the days of the 2.4 kernel. To develop the simple LED driver above, we used half a dozen abstractions: cdev, sysfs, kobjects, classes, class device, and parport. The abstractions, however, bring several advantages to the table such as bug-free building blocks, code reuse, and elegant design.

## RTC Subsystem

RTC support in the kernel is architected into two layers: a hardware-independent top-layer char driver that implements the kernel RTC API, and a hardware-dependent bottom-layer driver that communicates with the underlying bus. The RTC API, specified in *Documentation/rtc.txt*, is a set of standard ioctls that conforming applications such as hwclock leverage by operating on `/dev/rtc`. The API also specifies attributes in sysfs (`/sys/class/rtc/`) and procfs (`/proc/driver/rtc`). The RTC API guarantees that user space tools are independent of the underlying platform and the RTC chip. The bottom-layer RTC driver is bus-specific. The embedded device discussed in the section “Device Example: Real Time Clock” in Chapter 8, “The Inter-Integrated Circuit Protocol,” has an RTC chip connected to the I²C bus, which is driven by an I²C client driver.

The kernel has a dedicated RTC subsystem that provides the top-layer char driver and a core infrastructure that bottom-layer RTC drivers can use to tie in with the top layer. The main components of this infrastructure are the `rtc_class_ops` structure and the registration functions, `rtc_device_[register|unregister]()`. Bottom-layer RTC drivers scattered under different bus-specific directories are being unified with this subsystem under `drivers/rtc/`.

The RTC subsystem allows the possibility that a system can have more than one RTC. It does this by exporting multiple interfaces, `/dev/rtcN` and `/sys/class/rtc/rtcN`, where *N* is the number of RTCs on your system. Some embedded systems, for example, have two RTCs: one built in to the microcontroller to support sophisticated operations such as periodic interrupt generation, and another no-frills low-power battery-backed external RTC for timekeeping. Because RTC-aware applications operate over `/dev/rtc`, set up a symbolic link so that one of the created `/dev/rtcX` nodes can be accessed as `/dev/rtc`.

To enable the RTC subsystem, turn on `CONFIG_RTC_CLASS` during kernel configuration.

> **The Legacy PC RTC Driver**
>
> On PC systems, you have the option of bypassing the RTC subsystem by using the legacy RTC driver, `drivers/char/rtc.c`. This driver provides top and bottom layers for the RTC on PC-compatible systems and exports `/dev/rtc` and `/proc/driver/rtc` to user applications. To enable this driver, turn on `CONFIG_RTC` during kernel configuration.

## Pseudo Char Drivers

Several commonly used kernel facilities are not connected with any physical hardware, and these are elegantly implemented as char devices. The $null$ sink, the perpetual $zero$ source, and the kernel random number generator are treated as virtual devices and are accessed using $pseudo$ char device drivers.

The $/dev/null$ char device sinks data that you don't want to display on your screen. So if you need to check out source files from a Concurrent Versioning System (CVS) repository without spewing filenames all over the screen, do this:

```
bash> cvs co kernel > /dev/null
```

This redirects command output to the write entry point belonging to the $/dev/null$ driver. The driver's $read()$ and $write()$ methods simply return success ignoring the contents of the input and output buffers, respectively.

If you want to fill an image file with zeros, call upon $/dev/zero$ to come to your service:

```
bash> dd if=/dev/zero of=file.img bs=1024 count=1024
```

This sources a stream of zeros from the $read()$ method belonging to the $/dev/zero$ driver. The driver has no $write()$ method.

The kernel has a built-in random number generator. For the benefit of kernel users who desire to use random sequences, the random number generator exports APIs such as $get_random_bytes()$. For user mode programs, it exports two char interfaces: $/dev/random$ and $/dev/urandom$. The quality of randomness is higher for reads from $/dev/random$ compared to that from $/dev/urandom$. When a user program reads from $/dev/random$, it gets strong (or true) random numbers, but reads from $/dev/urandom$ yield pseudo random numbers. The $/dev/random$ driver does not use formulae to generate strong random numbers. Instead, it gathers "environmental noise" (interval between interrupts, key clicks, and so on) for maintaining a reservoir of disorder (called an $entropy\ pool$) that seeds the random stream. To see the kernel's $input$ subsystem (discussed in Chapter 7) contributing to the entropy pool when it detects a keyboard press or mouse movement, look at $input\_event()$ defined in $drivers/input/input.c$:

```
void
input_event(struct input_dev *dev, unsigned int type,
unsigned int code, int value)
{
/* ... */
add_input_randomness(type, code, value); /* Contribute to entropy
pool */
/* ... */
}
```

To see how the core interrupt handling layer contributes inter-interrupt periods to the entropy pool, look at $handle\_IRQ\_event()$ defined in $kernel/irq/handle.c$:

```
irqreturn_t handle_IRQ_event(unsigned int irq,
struct irqaction *action)
{
/* ... */
if (status & IRQF_SAMPLE_RANDOM)
```
