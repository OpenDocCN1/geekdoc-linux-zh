30 Chapter 2 • Hardware Basics

# Ports

Most PCs are equipped with both serial ports, which read or write one bit at a time, and parallel ports, which read or write one character at a time. This subsection explains Red Hat support for serial and parallel ports.

# Serial Ports

The standard Red Hat Linux kernel includes for 192 serial ports. However, by default, the device files /dev/ttyS0,/dev/ttyS1,/dev/ttyS2, and /dev/ttyS3 are created during the installation of Red Hat Linux. Documentation refers to serial ports as /dev/cua0;; however, this is an older, deprecated way of naming serial ports. You can increase the number of ports by modifying the file drivers/char/serial.c and recompiling the kernel.

You can generally use the BIOS to configure the IRQ and I/O port associated with serial ports ttyS0 and ttyS1. To configure additional ports, you can use the setserial command as follows:

```
setserial /dev/ttySn irq port y skip_test autoconfig
```

where ttySn specifies the serial port, x specifies the IRQ to be assigned, and y specifies the I/O port to be assigned.

> See the page for the setserial command to learn about other options that set the baud rate and other operating parameters.

# Parallel Ports

The standard Red Hat Linux kernel includes support for eight parallel ports. However, by default, the device files /dev/lp0, /dev/lp1, and /dev/1p2 are created during installation of Red Hat Linux. You can increase the number of ports by modifying the header file drivers/char/lp.c and recompiling the kernel. You can generally use the BIOS to configure the IRQ and I/O port associated with serial ports lp0 and 1p1. It is unusual to configure more than two parallel ports.

# Peripherals

This subsection describes Red Hat Linux support for common peripherals, including keyboards, mice, modems, network adapters, sound cards, and video cards.