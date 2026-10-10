Cold-pluggable devices are hardware that can be connected to the system only when the system is completely powered down. These usually include things commonly found inside the computer case, such as memory, PCI cards, and hard drives. You can't remove any of these things while the system is running.

Conversely, you can usually add and remove hot-pluggable devices at any time. They are often external components, such as network connections, monitors, and USB devices. The trick with hot-pluggable devices is that somehow the Linux kernel needs to know when the device is connected and automatically load the correct device driver module to support the device.

Linux provides an entire subsystem that interacts with hot-pluggable devices, making them accessible to users. This subsystem is described in the following sections.

# Detecting Dynamic Devices

The *udev device manager* is a program that is automatically started at boot time by the *init* process (usually at run level 5 via the */etc/rc5.d/udev* script) or the systemd systems and runs in the background at all times. It listens to kernel notifications about hardware devices. As new hardware devices are plugged into the running system, or existing hardware devices removed, the kernel sends out notification event messages.

The *udev* program listens to these notification messages and compares the messages against rules defined in a set of configuration files, normally stored under the */etc/udev/rules.d* directory. If a device matches a defined rule, *udev* acts on the event notification as defined by the rule.

Each Linux distribution defines a standard set of rules for *udev* to follow. Rules define actions such as mounting USB memory sticks under the */media* folder when they're installed or disabling network access when a USB network card is removed. You can modify the rules defined, but it's usually not necessary.

# Working with Dynamic Devices

While the *udev* program runs in the background on your Linux system, you can still interact with it using the *udevadm* command-line tool. The *udevadm* command allows you to send commands to the *udev* program. The format of the *udevadm* command is as follows:

```
udevadm command [options]
```

Table 23.3 shows the commands available to send to the *udevadm* program.

# TABLE 23.3  The udevadm commands

| Command | Description |
| :--- | :--- |
| *control* | Modifies the internal state of *udev* |
| *info* | Queries the *udev* database for device information |