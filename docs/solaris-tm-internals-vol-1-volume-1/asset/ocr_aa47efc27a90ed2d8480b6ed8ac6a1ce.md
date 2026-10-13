# **Table 1-2**  *File Systems Available in Solaris File System Framework (Continued)*

| File System | Type | Device | Description |
|---|---|---|---|
| `procfs` | Pseudo | Kernel | `/proc` file system representing processes |
| `sockfs` | Pseudo | Network | File system of socket connections |
| `fdfs` | Pseudo | File Descriptors | Allows a process to see its open files in `/dev/fd` |
| `fifofs` | Pseudo | Files | FIFO file system |

# ## 1.9  I/O Architecture

Traditional UNIX implements kernel-resident device drivers to interface with hardware devices. The device driver manages data transfer and register I/O and handles device hardware interrupts. A device driver typically has to know intimate details about the hardware device and the layout of buses to which the device is connected. Solaris extends traditional device driver management functions by using separate drivers for devices and buses: *a device driver* controls a device’s hardware, and *a bus nexus driver* controls and translates data between two different types of buses.

Solaris organizes I/O devices in a hierarchy of bus nexus and instances of devices, according to the physical connection hierarchy of the devices. The hierarchy shown in Figure 1.9 represents a typical Solaris *device tree*.

![](bbox=[0.148, 0.633, 0.794, 0.867])

# **Figure 1.9** *The Solaris Device Tree*