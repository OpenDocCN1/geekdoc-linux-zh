
## Table 5.4. Summary of Kernel Programming Interfaces

| Data Structure | Location | Description |
| :--- | :--- | :--- |
| poll_table | include/linux/poll.h | A table of wait queues owned by drivers that are being polled for data |
| pardevice | include/linux/parport.h | Kernel abstraction of a parallel port device |
| rtc_class_ops | include/linux/rtc.h | Communication interface between top layer and bottom layer RTC drivers |
| miscdevice | include/linux/miscdevice.h | Representation of a misc device |

| Kernel Interface | Location | Description |
| :--- | :--- | :--- |
| alloc_chrdev_region() | fs/char_dev.c | Requests dynamic allocation of a device major number |
| unregister_chrdev_region() | fs/char_dev.c | Reverse of alloc_chrdev_region() |
| cdev_init() | fs/char_dev.c | Connects char driver methods with the associated cdev |
| cdev_add() | fs/char_dev.c | Associates a device number with a cdev |
| cdev_del() | fs/char_dev.c | Removes a cdev |
| container_of() | include/linux/kernel.h | From a structure member, gets the address of its containing structure |
| copy_from_user() | arch/x86/lib/usercopy_32.c (For i386) | Copies data from user space to kernel space |
| copy_to_user() | arch/x86/lib/usercopy_32.c (For i386) | Copies data from kernel space to user space |
| likely() | include/linux/compiler.h | Informs GCC about the possibility of success of the associated conditional |
| unlikely() | include/linux/compiler.h | Informs GCC about the possibility of failure of the associated conditional evaluation |
| request_region() | include/linux/ioport.h, kernel/resource.c | Stakes claim to an I/O region |
| release_region() | include/linux/ioport.h, kernel/resource.c | Relinquishes claim to an I/O region |
| in[b\|w\|l\|sn\|sl]() | include/asm-your-arch/io.h | Family of functions to exchange data with I/O regions |
| out[b\|w\|l\|sn\|sl]() | include/asm-your-arch/io.h | Family of functions to exchange data with I/O regions |
| poll_wait() | include/linux/poll.h | Adds a wait queue to the kernel poll_table |
| fasync_helper() | fs/fcntl.c | Ensures that if a driver issues a kill_fasync(), a SIGIO is dispatched to the owning application |
| kill_fasync() | fs/fcntl.c | Dispatches a SIGIO to the owning application |
| parport_register_device() | drivers/parport/share.c | Registers a parallel port device with parport |
| parport_unregister_device() | drivers/parport/share.c | Unregisters a parallel port device |
| parport_register_driver() | drivers/parport/share.c | Registers a parallel port driver with parport |
| parport_unregister_driver() | drivers/parport/share.c | Unregisters a parallel port driver |
| parport_claim_or_block() | drivers/parport/share.c | Claims a parallel port |
| parport_write_data() | include/linux/parport.h | Writes data to a parallel port |
| parport_read_data() | include/linux/parport.h | Reads data from a parallel port |
| parport_release() | drivers/parport/share.c | Releases a parallel port |
| kobject_register() | lib/kobject.c | Registers a kobject and creates associated files in sysfs |
| kobject_unregister() | lib/kobject.c | Reverse of kobject_register() |
| rtc_device_register() / rtc_device_unregister() | drivers/rtc/class.c | Registers/unregisters a bottom-layer driver with the RTC subsystem |
| misc_register() | drivers/char/misc.c | Registers a misc driver |
| misc_deregister() | drivers/char/misc.c | Unregisters a misc driver |

# Chapter 6. Serial Drivers

## In This Chapter

- Layered Architecture 173
- UART Drivers 176
- TTY Drivers 192
- Line Disciplines 194
- Looking at the Sources 205

The serial port is a basic communication channel used by a slew of technologies and applications. A chip known as the *Universal Asynchronous Receiver Transmitter* (UART) is commonly used to implement serial communication. On PC-compatible hardware, the UART is part of the Super I/O chipset, as shown in Figure 6.1.

![](img/07cc6f9c8c74622020874f66bfb53dc4_161_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_162_0.png)

Though RS-232 communication channels are the common type of serial hardware, the kernel's serial subsystem is architectured in a generic manner to serve diverse users. You will touch the serial subsystem if you

- Run a terminal session over an RS-232 serial link
- Connect to the Internet via a dialup, cellular, or software modem
- Interface with devices such as touch controllers, smart cards, Bluetooth chips, or Infrared dongles, which use a serial transport
- Emulate a serial port using a USB-to-serial converter
- Communicate over an RS-485 link, which is a multidrop variant of RS-232 that has larger range and better noise immunity

In this chapter, let's find out how the kernel structures the serial subsystem. We will use the example of a Linux cell phone to learn about low-level UART drivers and the example of a serial touch controller to discover the implementation details of higher-level line disciplines.

The UART usually found on PCs is National Semiconductor's 16550, or compatible chips from other vendors, so you will find references to "16550-type UART" in code and documentation. The 8250 chip is the predecessor of the 16550, so the Linux driver for PC UARTs is named **8250.c**.

## Layered Architecture

As you just saw, the users of the serial subsystem are many and different. This has motivated kernel developers to structure a layered serial architecture using the following building blocks:

1. Low-level drivers that worry about the internals of the UART or other underlying serial hardware.
2. A tty driver layer that interfaces with the low-level driver. A tty driver insulates higher layers from the intricacies of the hardware.
3. Line disciplines that "cook" data exchanged with the tty driver. Line disciplines shape the behavior of the serial layer and help reuse lower layers to support different technologies.

To help custom driver implementations, the serial subsystem also provides core APIs that factor commonalities out of these layers.

**Figure 6.2** shows the connection between the layers. N_TTY, N_IRDA, and N_PPP are drop-in line disciplines that mold the serial subsystem to respectively support terminals, Infrared, and dialup networking. **Figure 6.3** maps the serial subsystem to kernel source files.

### Figure 6.2. Connection between the layers in the serial subsystem.

![](img/07cc6f9c8c74622020874f66bfb53dc4_164_0.png)

### Figure 6.3. Serial layers mapped to kernel sources.

![](img/07cc6f9c8c74622020874f66bfb53dc4_165_0.png)

To illustrate the advantages of a layered serial architecture, let's use an example. Assume that you are using a USB-to-serial adapter to obtain serial capabilities on a laptop that does not have a serial port. One possible scenario is when you are debugging the kernel on a target embedded device from a host laptop using kgdb (kgdb is discussed in Chapter 21, "Debugging Device Drivers"), as shown in Figure 6.4.

### Figure 6.4. Using a USB-to-serial converter.

![](img/07cc6f9c8c74622020874f66bfb53dc4_165_1.png)

As shown in Figure 6.3, you first need a suitable USB physical layer driver (the USB counterpart of the UART driver) on your host laptop. This is present in the kernel USB subsystem, `drivers/usb/`. Next, you need a tty driver to sit on top of the USB physical layer. The usbserial driver (`drivers/usb/serial/usb-serial.c`) is the core layer that implements a generic tty over USB-serial converters. This driver, in tandem with device-specific tty methods registered by the converter driver (`drivers/usb/serial/keyspan.c` if you are using a Keyspan adapter, for example), constitutes the tty layer. Last, but not the least, you need the N_TTY line discipline for terminal I/O processing.

The tty driver insulates the line discipline and higher layers from the internals of USB. In fact, the line discipline still thinks it's running over a conventional UART. This is so because the tty driver pulls data from USB Request Blocks or URBs (discussed in Chapter 11, "Universal Serial Bus") and encapsulates it in the format expected by the N_TTY line discipline. The layered architecture thus renders the implementation simpler—all blocks from the line discipline upward can be reused unchanged.

The preceding example uses a technology-specific tty driver and a generic line discipline. The reverse usage is also common. The Infrared stack, discussed in Chapter 16, "Linux Without Wires," uses a generic tty driver and a technology-specific line discipline called N_IRDA.

As you might have noticed in Figure 6.2 and Figure 6.3, although UART drivers are char drivers, they do not directly expose interfaces to kernel system calls like regular char drivers that we saw in the preceding chapter. Rather, UART drivers (like keyboard drivers discussed in the next chapter) service another kernel layer, the tty layer. I/O system calls start their journey above top-level line disciplines and finally ripple down to UART drivers through the tty layer.

In the rest of this chapter, let's take a closer look at the different driver components of the serial layer. We start at the bottom of the serial stack with low-level UART drivers, move on to middle-level tty drivers, and then proceed to top-level line discipline drivers.
