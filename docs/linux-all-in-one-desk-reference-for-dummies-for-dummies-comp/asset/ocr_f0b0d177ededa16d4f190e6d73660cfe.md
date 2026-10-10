# Understanding Linux Devices

Linux treats all devices as files and uses a device just as it uses a file — opens it, writes data to it, reads data from it, and closes it when done. This ability to treat every device as a file comes through the use of device drivers. A *device driver* is a special program that controls a particular type of hardware. When the kernel writes data to the device, the device driver does whatever is appropriate for that device. For example, when the kernel writes data to the floppy drive, the floppy device driver puts that data onto the physical medium of the floppy disk. On the other hand, if the kernel writes data to the parallel port device, the parallel port driver sends the data to the printer connected to the parallel port.

Thus the device driver isolates the device-specific code from the rest of the kernel and makes a device look like a file. Any application can access a device by opening the file specific to that device. Figure 1-7 illustrates this concept of a Linux device driver.

**Figure 1-7:** An application can access a device through a special file that, in turn, uses a device driver.

![](bbox=[0.25, 0.45, 0.78, 0.7])

# **Device files**

As Figure 1-7 shows, applications can access a device as if it were a file. These files are special files called *device files*, and they appear in the `/dev` directory in the Linux file system.