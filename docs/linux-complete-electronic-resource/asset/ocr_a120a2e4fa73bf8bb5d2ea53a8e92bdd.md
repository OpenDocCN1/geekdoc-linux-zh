Some of these cards require software to be downloaded to them to make them operational. There is a separate utility to do this with.

Full details on how to configure the Linux ISDN support are available from the `/usr/src/linux/Documentation/isdn/` directory, and a FAQ dedicated to *isdn4linux* is available at www.1rz-muenchen.de (see http://www.1rz-muenchen.de/‘ui161lab/www/isdn/ ). (You can click the English flag to get an English version.)

A note about PPP. The PPP suite of protocols will operate over either asynchronous or synchronous serial lines. The commonly distributed PPP daemon for Linux “pppd” supports only asynchronous mode. If you wish to run the PPP protocols over your ISDN service you need a specially modified version. Details of where to find it are available in the documentation referred to above.

# PLIP for Linux 2

PLIP device names are “plip0,” “plip1,” and “plip2.”

# Kernel Compile Options:

```
Network device support ---
<> PLIP (parallel port) support
```

PLIP (Parallel Line IP), is like SLIP, in that it is used for providing a *point-to-point* network connection between two machines. However, it is designed to use the parallel printer ports on your machine instead of the serial ports (a cabling diagram is included in the cabling diagram section later in this document). Because it is possible to transfer more than one bit at a time with a parallel port, it is possible to attain higher speeds with the PLIP interface than with a standard serial device. In addition, even the simplest of parallel ports, printer ports, can be used in lieu of having to purchase comparatively expensive 16550AFN UARTs for your serial ports. PLIP uses a lot of CPU compared to a serial link and is most certainly not a good option if you can obtain some cheap Ethernet cards. But it will work when nothing else is available and will work quite well. You should expect a data transfer rate of about 20 kilobytes per second when a link is running well.

The PLIP device driver competes with the parallel device driver for the parallel port hardware. If you wish to use both drivers, then you should compile them both as modules to ensure that you are able to select which port you want to use for PLIP and which ports you want for the printer driver. Refer to the “Modules mini-HOWTO” for more information on kernel module configuration.