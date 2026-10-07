# Chapter 13 Printers and the Spooling Subsystem

next. When the lp1 driver is built into the kernel, the kernel will accept through LILO
1p= option to set interrupts and I/O addresses.

Syntax:

```
1p=port0,[irq0,port1,[irq1,[port2,[irq2]]]
```

Example:

```
1p=0x3bc,10,0x278,5,0x378
```

This example will set up three PC-style ports, one at 0x3bc with an IRQ of 10, one at
0x278 with an IRQ of 5, and one at 0x378 using IRQ 7. Some systems will have only one
parallel port set up in this way.

# The parport Device

The parport device was added to kernels 2.1.33 and newer to connect several of the prob-
lems that in the old lp device driver. The parport device can share the ports
bween multiple device drivers and dynamically assign available parallel ports to device
numbers than simply equating an I/O address with a specific port number: a printer
of the first parallel port might not be assigned /dev/lp using port. The development
of parport device brought about the capability to run many devices via the par-
ell port, including Zip drives, Backpack CD-ROMs, and external hard disks. It is pos-
sible to share a single parallel port among several devices, and all the corresponding
drivers may be compiled into the kernel.

You must have CONFIG_PARPORT and CONFIG_PARPORT_PC set to YES in your kernel con-
figuration if your parallel port is PC compatible (all IBM-compatibles and some Alpha
machine PC-style parallel ports). If your printer is not serial, you must have
CONFIG_PRINTER set to YES in your kernel configuration. Use the same terms as listed
above for checking printing support.

# RS-232 Serial Devices

A printer attached to a standard RS-232 serial port requires only that the serial port be
enabled and the printcap entry be set up correctly. Serial support is almost always
built into the kernel by default to accommodate modems and other serial devices, and
these ports supporting printing capability as well. Chapter 12 discusses Linux support for
RS-232 serial connections.

# USB Devices

USB printers require special attention in Linux, because of the need for USB-patched
2.2.x or 2.4.x kernels. In particular, you need both basic USB support (including support

![](bbox=[0.082, 0.135, 0.235, 0.735])