
into 30 discrete 64kbps B channels with one 64kbps D channel. Any number of channels may be used at a time and in any combination. You could, for example, establish 30 separate calls to 50 different destinations at 64kbps each, or you could establish 15 calls to 15 different destinations at 128kbps each (two channels used per call), or just a small number of calls and leave the rest idle. A channel may be used for either incoming or outgoing calls. The original intention of ISDN was to allow telecommunications companies to provide a single data service that could deliver either telephone (via digitized voice) or data services to your home or business without requiring you to make any special configuration changes.

There are a few different ways to connect your computer to an ISDN service. One way is to use a device called a “Terminal Adaptor,” which plugs into the Network Terminating Unit that your telecommunications carrier installed when you got your ISDN service and which presents a number of serial interfaces. One of those interfaces is used to enter commands to establish calls and configuration, and the others are actually connected to the network devices that will use the data circuits when they are established. Linux will work on this sort of configuration without modification; you just treat the port on the Terminal Adaptor like you would treat any other serial device. Another way, which is what the kernel ISDN support is designed for, allows you to install an ISDN card into your Linux machine and then has your Linux software handle the protocols and make the calls itself.

## Kernel Compile Options:

```
ISDN subsystem -->
<> ISDN support
[] Support synchronous PPP
[] Support audio via ISDN
< ICN 2B and 4B support
<> PCBIT-D support
<> Teles/NIccy1016PC/Creatix support
```

The Linux implementation of ISDN supports a number of different types of internal ISDN cards. These are those listed in the kernel configuration options:

- ICN 2B and 4B
- Octal PCBIT-D
- Teles ISDN-cards and compatibles

Some of these cards require software to be downloaded to them to make them operational. There is a separate utility to do this with.

Full details on how to configure the Linux ISDN support are available from the `/usr/src/linux/Documentation/isdn/` directory, and a FAQ dedicated to *isdn4linux* is available at www.1rz-muenchen.de (see http://www.1rz-muenchen.de/ui161lab/www/isdn/ ). (You can click the English flag to get an English version.)

A note about PPP. The PPP suite of protocols will operate over either asynchronous or synchronous serial lines. The commonly distributed PPP daemon for Linux “pppd” supports only asynchronous mode. If you wish to run the PPP protocols over your ISDN service you need a specially modified version. Details of where to find it are available in the documentation referred to above.

# PLIP for Linux 2

PLIP device names are “plip0,” “plip1,” and “plip2.”

## Kernel Compile Options:

```
Network device support ---
<> PLIP (parallel port) support
```

PLIP (Parallel Line IP), is like SLIP, in that it is used for providing a *point-to-point* network connection between two machines. However, it is designed to use the parallel printer ports on your machine instead of the serial ports (a cabling diagram is included in the cabling diagram section later in this document). Because it is possible to transfer more than one bit at a time with a parallel port, it is possible to attain higher speeds with the PLIP interface than with a standard serial device. In addition, even the simplest of parallel ports, printer ports, can be used in lieu of having to purchase comparatively expensive 16550AFN UARTs for your serial ports. PLIP uses a lot of CPU compared to a serial link and is most certainly not a good option if you can obtain some cheap Ethernet cards. But it will work when nothing else is available and will work quite well. You should expect a data transfer rate of about 20 kilobytes per second when a link is running well.

The PLIP device driver competes with the parallel device driver for the parallel port hardware. If you wish to use both drivers, then you should compile them both as modules to ensure that you are able to select which port you want to use for PLIP and which ports you want for the printer driver. Refer to the “Modules mini-HOWTO” for more information on kernel module configuration.

Please note that some laptops use chipsets that will not work with PLIP because they do not allow some combinations of signals that PLIP relies on, that printers don’t use.

The Linux PLIP interface is compatible with the *Craynwr Packet Driver PLIP*, and this will mean that you can connect your Linux machine to a DOS machine running any other sort of tcp/ip software via PLIP.

In the 2.0.* series kernel the PLIP devices are mapped to i/o port and IRQ as follows:

| device | i/o | IRQ |
|---|---|---|
| plip0 | 0x3bc | 5 |
| plip1 | 0x378 | 7 |
| plip2 | 0x278 | 2 |

If your parallel ports don’t match any of the above combinations, then you can change the IRQ of a port using the *ifconfig* command and the “*i*rq=” parameter (be sure to enable IRQs on printer ports in your ROM BIOS if it supports this option). As an alternative, you can specify “*i*o=” and “*i*rq=” options on the *insmod* command line, if you use modules. For example:

```
root# insmod plip.o io=0x288 irq=5
```

PLIP operation is controlled by two timeouts, whose default values are probably ok in most cases. You will probably need to increase them if you have an especially slow computer, in which case *the timers to increase are actually on the other machine*. A program called *plipconf* exists that allows you to change these timer settings without recompiling your kernel. It is supplied with many Linux distributions.

To configure a PLIP interface, you will need to invoke the following commands (or add them to your initialization scripts):

```
root# /sbin/ifconfig plip1 localplip pointopoint remoteplip
root# /sbin/route add remotelip plip1
```

Here, the port being used is the one at I/O address 0x378; *localplip* and *remoteplip* are the names or IP addresses used over the PLIP cable. I personally keep them in my */etc/hosts* database:

```
# plip entries
192.168.3.1 localplip
192.168.3.2 remoteplip
```

The *pointopoint* parameter has the same meaning as for SLIP, in that it specifies the address of the machine at the other end of the link.

Part III

In almost all respects you can treat a *PLIP* interface as though it were a *SLIP* interface, except that neither *dip* nor *slattach* need be, nor can be, used.

Further information on PLIP may be obtained from the “PLIP mini-HOWTO.”

## PLIP for Linux-2.2

During development of the 2.1 kernel versions, support for the parallel port was changed to a better setup.

**Kernel Compile Options:**

```
General setup -->
[ ] Parallel port support
Network device support -->
<*> PLIP (parallel port) support
```

The new code for PLIP behaves like the old one. Use the same *ifconfig* and *route* commands as in the previous section, but initialization of the device is different due to the advanced parallel port support.

The “first” PLIP device is always called “*plip0*,” where *first* is the first device detected by the system, similar to what happens for Ethernet devices. The actual parallel port being used is one of the available ports, as shown in `/proc/parport`. For example, if you have only one parallel port, you’ll only have a directory called `/proc/parport/0`.

If your kernel didn’t detect the IRQ number used by your port, “`insmod plip`” will fail; in this case just write the right number to `/proc/parport/0/irq` and reinvoke *insmod*.

Complete information about parallel port management is available in the file `Documentation/parport.txt`, part of your kernel sources.

## PPP

PPP devices names are “*ppp0*,” “*ppp1*,” etc. Devices are numbered sequentially with the first device configured receiving “0.”

**Kernel Compile Options:**

```
Networking options -->
<*> PPP (point-to-point) support
```

PPP configuration is covered in detail in the PPP-HOWTO (see PPP-HOWTO.html).
