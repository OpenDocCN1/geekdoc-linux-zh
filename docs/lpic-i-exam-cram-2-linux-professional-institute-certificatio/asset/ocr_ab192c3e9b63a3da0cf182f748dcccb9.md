# Plug and Play

When Plug and Play (PnP) is used, a device usually configures itself when plugged into the system bus. Plug and Play helps match drivers and devices with the correct communication mechanisms.

Linux isn't truly a Plug and Play OS, but the kernel does read the registers for the devices on the system, many of which can be easily recognized and made available to the device drivers via a table managed by the kernel.

The kernel does provide programmatic help to drivers in the form of programs and code that do PnP, and typically that's enough to get the device working. The kernel also assists in keeping resource conflicts from occurring by restricting bus resources to a single device. The 2.2 kernel provided this only for the IRQ and DMA resources, but the 2.4 kernel now provides this support for I/O addresses as well.

> **NOTE** Most BIOSs are PnP-compatible, and if the BIOS reads the device and then the kernel can see it from there, it's not really PnP, but it works.

# PnP Tools

The main utility for configuring devices under Linux is the `isapnp` program. Part of the isapnp tools suite, it's run at startup on many Linux distributions to discover the resources located on the ISA bus using software. (Remember that the PCI bus typically discovers devices using hardware and then makes those devices available to Linux.)

isapnp is configured with the `/etc/isapnp.conf` file, consisting of a custom mapping of which devices are going to use which resources on the system.

pnpdump reads the devices on the ISA bus and dumps that information out to the console by default. You can use pnpdump to view the configuration of a device and then edit `isapnp.conf` to add a similar device to the system, particularly if that device was not recognized properly.

> **ALERT** Thankfully, LPI doesn't think that we should be delving into the `isapnp.conf` file or the gory details of PnP outside of the concept, needed files, and commands we have covered here.