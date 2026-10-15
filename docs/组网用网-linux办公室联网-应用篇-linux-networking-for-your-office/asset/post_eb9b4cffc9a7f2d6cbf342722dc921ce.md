
ISPs also differ in how well they handle all the assorted services they provide. Some are rock-solid and seldom experience service outages. Others provide unreliable service—connection difficulties, poor news servers, and so on. Many ISPs offer a free trial period, so if you’re dissatisfied with the service in the first month or so, you can change without having expended money on the ISP. You can also consult with your friends, neighbors, and co-workers about the reliability of different ISPs.

> Because you reach your ISP via a telephone connection, your phone company might charge you for each telephone call. You should be sure that your chosen ISP has at least one number that’s within your local calling area, or be prepared to pay your phone company for your online time. If you have metered phone service, you’ll be charged for all phone calls, including those to your ISP. Many companies and individuals who make heavy calls of Internet access pay for dedicated phone lines for this access, which can easily at least double or triple the monthly costs.

## Configuring Your Serial Ports

After you’ve selected an ISP, it’s time to begin configuring Linux to use that ISP. Because PPP works over modems, and hence over serial lines, your Linux configuration task begins with configuring your serial ports.

> Traditionally, even internal modems have used serial ports. To Linux, these modems are indistinguishable from external modems. Many recent internal modems are Windows-only devices, however, which don’t use conventional serial ports. As of this writing, no such devices are usable from Linux. For more information on modems, see Chapter 1, “Networking Hardware.”

## Setting Kernel Options

For information on how to configure and compile your kernel, see Chapter 6, “Compiling a Kernel for Networking.” Red Hat 6.0 comes with the necessary support precompiled for most PPP configurations, but if you want or need to recompile your kernel, you should ensure that the necessary options are included.

There are two kernel options you must enable to use PPP networking via a serial port modem:

- Serial port support—In most cases, this is the Standard/generic (dumb) serial support option under the Character devices configuration menu. This option provides access to the serial ports that are built in to modern motherboards, and to the ports that are used on conventional internal modems. If you’re using a multiport serial board, though, you’ll need to enable the Non-standard serial port support option and the appropriate specific board’s driver in addition to or instead of the standard support.
- PPP support—You activate PPP support by selecting PPP (point-to-point) support from the Network device support configuration menu.

In addition to these two items, you need the usual TCP/IP configuration options. If you plan to use the dial-on-demand feature described later in this chapter, you must also compile in the SLIP (serial line) support option, which in 2.2-series kernels is located just below the PPP option, and the IP: Transparent Proxy Support option under the Networking options heading. Dial-on-demand lets your computer make a PPP connection whenever outgoing network traffic appears. This can be a very useful feature if you want your Linux computer to perform IP masquerading for a local network, as described in Chapter 20, “One IP Address, Many Computers: IP Masquerading.”

### Tip

Because most computers are connected by using PPP only a small portion of the time, you can compile the serial line, PPP, and (if you need it) Serial Line Internet Protocol (SLIP) options as modules. This will save on memory when PPP isn’t in use.

You can check that your system includes PPP support in the kernel by typing /usr/sbin/pppd. If the system returns a message to the effect that PPP support is not present, then you need to recompile the kernel or ensure that the PPP support module is loaded. If everything is configured properly, the system will return some gibberish, like this:

```
-y}j#@!|])|}] }4}*}&} } } } }&0*_}i'_}*}('v)*~-
```

This is the PPP protocol trying to negotiate a link with the screen, which of course fails, so after a minute or two of printing a burst of gibberish every few seconds, pppd gives up and returns control to you.
