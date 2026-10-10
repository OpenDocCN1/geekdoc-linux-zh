
## Code View

```
/sys
  +block
  -[bus]-[sb]-[devices]-[usb2]-[2-2]-[2-2:1.0]-[usbendpoint:usbdev2,2-ep81]
  -[class]-[input]-[mouse2]-[devic2]-[bus]-[usbendpoint:usbdev2,2-ep81]
      -[usb_device]-[usbdev2]-[device]-[bus]
      -[usb_endpoint]-[usbdev2,2-ep00]-[device]
          -[usbdev2,2-ep81]-[device]
  -[devices]-[pci0000:00]-[0000:00:1d:11]-[usb2]-[2-2]-[2-2:1.0]
  +[firmware]
  +[fs]
  +[kernel]
  +[module]
  +[power]
```

Browse through /sys looking for entries that associate with another device (for example, your network card) to get a better feel of its hierarchical organization. The section "Addressing and Identification" in Chapter 10 illustrates how sysfs mirrors the physical connection of a CardBus Ethernet-Modem card on a laptop.

The class programming interface is built on top of kobjects and sysfs, so it's a good place to start digging to understand the end-to-end interactions between the components of the device model. Let's turn to the RTC driver for an example. The RTC driver (`drivers/char/rtc.c`) is a miscellaneous (or "misc") driver. We discuss misc drivers in detail when we look at character device drivers in Chapter 5.

Insert the RTC driver module and look at the nodes created under /sys and /dev:

```
bash> modprobe rtc
bash> ls -lR /sys/class/misc
drwxr-xr-x 2 root root 0 Jan 15 01:23 rtc
/sys/class/misc/rtc:
total 0
-rw-r--r-- 1 root root 4096 Jan 15 01:23 dev
-w------- 1 root root 4096 Jan 15 01:23 uevent
bash> ls -l /dev/rtc
crw-r--r-- 1 root root 10, 135 Jan 15 01:23 /dev/rtc
```

/sys/class/misc/rtc/dev contains the major and minor numbers (discussed in the next chapter) assigned to this device, /sys/class/misc/rtc/uevent is used for coldplugging (discussed in the next section), and /dev/rtc is used by applications to access the RTC driver.

Let's understand the code flow through the device model. Misc drivers utilize the services of `misc_register()` during initialization, which looks like this if you peel off some code:

```c
/* ... */
dev = MKDEV(MISC_MAJOR, misc->minor);

misc->class = class_device_create(misc_class, NULL, dev,
                                  misc->dev,
                                  "%s", misc->name);
if (IS_ERR(misc->class)) {
    err = PTR_ERR(misc->class);
    goto out;
}
/* ... */
```

Figure 4.5 continues to peel off more layers to get to the bottom of the device modeling. It illustrates the transitions that ripple through classes, kobjects, sysfs, and udev, which result in the generation of the /sys and /dev files listed previously.

### Figure 4.5. Tying the pieces of the device model.

![](img/07cc6f9c8c74622020874f66bfb53dc4_109_0.png)

Look at the parallel port LED driver (Listing 5.6 in the section "Talking to the Parallel Port" in Chapter 5) and the virtual mouse input driver (Listing 7.2 in the section "Device Example: Virtual Mouse" in Chapter 7) for examples on creating device control files inside sysfs.

Another abstraction that is part of the device model is the *bus-device-driver* programming interface. Kernel device support is cleanly structured into buses, devices, and drivers. This renders the individual driver implementations simpler and more general. *Bus* implementations can, for example, search for drivers that can handle a particular device.

Consider the kernel's I²C subsystem (explored in Chapter 8, "The Inter-Integrated Circuit Protocol"). The I²C layer consists of a core infrastructure, device drivers for bus adapters, and drivers for client devices. The I²C core layer registers each detected I²C bus adapter using `bus_register()`. When an I²C client device (say, an *Electrically Erasable Programmable Read-Only Memory* [EEPROM] chip) is probed and detected, its existence is recorded via `device_register()`. Finally, the I²C EEPROM client driver registers itself using `driver_register()`. These registrations are performed indirectly using service functions offered by the I²C core.

`bus_register()` adds a corresponding entry to /sys/bus/, while `device_register()` adds entries under /sys/devices/. `struct bus_type`, `struct device`, and `struct device_driver` are the main data structures used respectively by buses, devices, and drivers. Take a peek inside `include/linux/device.h` for their definitions.

## Hotplug and Coldplug

Devices connected to a running system on-the-fly are said to be hotplugged, whereas those connected prior to system boot are considered to be coldplugged. Earlier, the kernel used to notify user space about hotplug events by invoking a helper program registered via the /proc filesystem. But when current kernels detect hotplug, they dispatch uevents to user space via netlink sockets. Netlink sockets are an efficient mechanism to communicate between kernel space and user space using socket APIs. At the user-space end, udevd, the daemon that manages device node creation and removal, receives the uevents and manages hotplug.

To see how hotplug handling has evolved recently, let's consider progressive levels of udev running different versions of the 2.6 kernel:

- 1. With a *udev-039* package and a 2.6.9 kernel, when the kernel detects a hotplug event, it invokes the user space helper registered with `/proc/sys/kernel/hotplug`. This defaults to `/sbin/hotplug`, which receives attributes of the hotplugged device in its environment. `/sbin/hotplug` looks inside the hotplug configuration directory (usually `/etc/hotplug.d/default/`) and runs, for example, `/etc/hotplug.d/default/10-udev.hotplug`, after executing other scripts under `/etc/hotplug/`.

    ```bash
    bash$ ls -l /etc/hotplug.d/default/
    ...
    lrwxrwxrwx 1 root root 14 May 11 2005 10-udev.hotplug -> /sbin/udevsend
    ...
    ```

    When `/sbin/udevsend` thus gets executed, it passes the hotplugged device information to udevd.

- 2. With udev-058 and a 2.6.11 kernel, the story changes somewhat. The udevsend utility replaces `/sbin/hotplug`:

    ```bash
    bash$ cat /proc/sys/kernel/hotplug
    /sbin/udevsend
    ```

- 3. With the latest levels of udev and the kernel, udevd assumes full responsibility of managing hotplug without depending on udevsend. It now pulls hotplug events directly from the kernel via netlink sockets (see Figure 4.4). `/proc/sys/kernel/hotplug` contains nothing:

    ```bash
    bash$ cat /proc/sys/kernel/hotplug
    bash$
    ```

Udev also handles coldplug. Because udev is part of user space and is started only after the kernel boots, a special mechanism is needed to emulate hotplug events over coldplugged devices. At boot time, the kernel creates a file named `uevent` under `sysfs` for all devices and emits coldplug events to those files. When udev starts, it reads all the `uevent` files from `/sys` and generates hotplug events for each coldplugged device.

## Microcode Download

You have to feed microcode to some devices before they can get ready for action. The microcode gets executed by an on-card microcontroller. Device drivers used to store microcode inside static arrays in header files. But this has become untenable because microcode is usually distributed as proprietary binary images by device vendors, and that doesn't mix homogeneously with the GPL-ed kernel. Another reason against mixing firmware with kernel sources is that they run on different release time lines. The solution apparently is to separately maintain microcode in user space and pass it down to the kernel when required. Sysfs and udev provide an infrastructure to achieve this.

Let's take the example of the Intel PRO/Wireless 2100 WiFi mini PCI card found on several laptops. The card is built around a microcontroller that needs to execute externally supplied microcode for normal operation. Let's walk through the steps that the Linux driver follows to download microcode to the card. Assume that you have obtained the required microcode image (`ipw2100-1.3.fw`) from `http://ipw2100.sourceforge.net/firmware.php` and saved it under `/lib/firmware/` on your system and that you have inserted the driver module `ipw2100.ko`.

- 1. During initialization, the driver invokes the following:

    ```
    request_firmware(..., "ipw2100-1.3.fw", ...);
    ```

- 2. This dispatches a hotplug uevent to user space, along with the identity of the requested microcode image.

- 3. Udevd receives the uevent and responds by invoking `/sbin/firmware_helper`. For this, it uses a rule similar to the following from a file under `/etc/udev/rules.d/`:

    ```
    ACTION=="add", SUBSYSTEM=="firmware", RUN="/sbin/firmware_helper"
    ```

- 4. `/sbin/firmware_helper` looks inside `/lib/firmware/` and locates the requested microcode image `ipw2100-1.3.fw`. It dumps the image to `/sys/class/0000:02:02.0/data`. (`0000:02:02` is the PCI bus:device:function identifier of the WiFi card in this case.)

- 5. The driver receives the microcode and downloads it onto the device. When done, it calls `release_firmware()` to free the corresponding data structures.

- 6. The driver goes through the rest of the initializations and the WiFi adapter beacons.

## Module Autoload

Automatically loading kernel modules on demand is a convenient feature that Linux supports. To understand how the kernel emits a "module fault" and how udev handles it, let's insert a Xircom CardBus Ethernet adapter into a laptop's PC Card slot.
