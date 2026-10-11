
![](img/860d0c38bd76c9ded976e9d1e179ef25_429_0.png)

PS/2 mice almost always follow the same set of basic protocols, so you can swap PS/2 mice between computers without too much worry that they’ll work. Recent *wheel mice*, however, which use wheels to facilitate scrolling, often require a somewhat different driver to provide access to their wheel features. I describe these issues later in this chapter, in “Configuring a Pointer in Linux.”

Some mice come with adapters to let them function on either of two or more interfaces, such as serial and PS/2, or USB and PS/2. These adapters are often specific to one brand or model of mouse, so you might not be able to swap an adapter from one mouse to another.

The PS/2 mouse port consumes its own interrupt (IRQ 12). You can often disable this port—and therefore free IRQ 12—in the computer’s BIOS, if you’re not using a PS/2 mouse. Doing so can be worthwhile if you’re short on IRQs and need a USB device for some other purpose. Switching from a PS/2 mouse to a serial mouse won’t normally save an interrupt, because the serial port requires its own interrupt. (An exception would be if you use an advanced multiport serial card that consumes only one interrupt no matter how many devices are in use. Such cards are normally used only on systems that need many serial ports, such as computers used to accept many dial-in modem connections.) If you have some other device that you must configure for IRQ 12, however, switching from a PS/2 mouse to a serial mouse can make sense. The PS/2 port is very inflexible in its interrupt requirements, whereas you can often adjust the serial port’s IRQs somewhat more.

### BusMouse Ports

In the late 1980s and early 1990s, a type of mouse known as a *bus mouse* was mildly popular. These mice used their own specialized mouse port, which was typically handled on a plug-in ISA card. The bus mouse interface looks much like the interface for PS/2 mice, but it’s electrically incompatible. You’re unlikely to encounter a bus mouse on a modern computer, unless the mouse has been salvaged from an older computer.

### Serial Ports

Conventional serial ports—more properly referred to as *RS-232* serial ports—were the most common way to attach mice to x86 computers through the mid-1990s. The serial port is a general-purpose port, and so can be used for many devices, albeit only one device per port. For this reason, most computers came with, and many still include, two RS-232 ports. Some computers, though, have only one RS-232 port.

Modern computers use 9-pin serial port connectors, as shown in Figure 15.1. Many older computers used at least one larger 25-pin connector, however. As with the full-size 5-pin DIN and smaller PS/2 keyboard connectors, adapters are available to connect 9-pin devices to 25-pin plugs, and vice versa. Figure 15.3 shows a 9-pin serial cable and a 9-pin-to-25-pin adapter. Despite the reduction in the number of pins, the 9-pin variety of serial port can be used for almost all the same tasks as can the 25-pin port; the additional 16 pins don’t add any substantial functionality, and certainly nothing that’s used by mice.

![](img/860d0c38bd76c9ded976e9d1e179ef25_430_0.png)

**FIGURE 15.3**  
*Serial connectors come in 9- and 25-pin varieties, and adapters let you convert from one type to another.*

One of the reasons for the demise of 25-pin connectors on motherboards is the similarity of these connectors to 25-pin parallel port connectors. Serial and parallel ports differ in gender, however. On the computer side, parallel ports use a male connector on the cable and a female connector on the computer. For serial ports, this relationship is reversed. Because the cables used by serial mice are permanently attached to the mouse, you needn’t be concerned with the gender of mouse cables on the mouse end.

A wide variety of serial mouse protocols have emerged over the years, the most common of these being Microsoft, Logitech, and Mouse Systems, each named after the company that originated the standard. Some mice support more than one protocol by use of a switch on the mouse's bottom or side. You select the mouse protocol you want to use at some point during Linux installation. If you choose the wrong protocol or change your mouse after installing Linux, you might need to adjust your XFree86 configuration, as described later in this chapter.

### USB Ports

*Universal Serial Bus (USB)* is the latest craze in external device connectors. USB is substantially faster than RS-232 serial, which is a great boon for many applications. Mice and keyboards, though, require relatively little in the way of speed, so USB's speed improvements aren't terribly important for these applications. USB does have other advantages, though. Most importantly, all the USB devices attached to a computer (up to 127) consume a single interrupt. In theory, then, switching from a standard keyboard and PS/2 or serial mouse to USB devices can save you an interrupt, because you need only one interrupt rather than two for these devices. Unfortunately, the standard PC keyboard interrupt is so deeply engrained in the PC architecture that it's impossible to disable it on most computers, even when a USB keyboard is used instead. If you have other USB devices, however, such as a USB digital camera or modem, you might be able to save an interrupt by putting your mouse on the USB port, as well.

![](img/860d0c38bd76c9ded976e9d1e179ef25_431_0.png)

> USB keyboards and mice are more common in the Macintosh market, so you might find a greater selection of these devices in the Macintosh section of your local computer superstore. Macintosh keyboards have slightly different keys than do PC keyboards, though. Specifically, Macintosh keyboards have no Windows key, and they have a Command key (imprinted with a cloverleaf design) instead of an Alt key. This difference is largely cosmetic. A bonus to buying a Macintosh USB keyboard is that Macintosh USB keyboards usually include a 2-port USB hub, which increases the number of USB devices you can attach to your computer. Macintosh USB mice should work fine on x86 hardware, but many of these devices have only one button, which is insufficient for Linux.

Linux's USB support is rudimentary at best in the 2.2.x kernels. The 2.3.x development kernels include support for many USB devices, so the 2.4.x kernel will almost certainly include stable USB support. Fortunately, USB keyboards and mice were some of the first USB devices to gain support in Linux, so these devices are well supported. Unfortunately, this support is still fairly new, so many x86 distributions don’t support USB keyboards and mice during installation. If you want to use a USB keyboard or mouse, therefore, you might need to install Linux using conventional devices and then swap in the USB devices after you’ve installed Linux and perhaps recompiled the kernel. Fortunately, this situation is likely to improve in the near future, so you should check your distribution’s list of supported hardware to see if USB devices are supported from the start.

One protocol supports all USB keyboards, and another supports all USB mice. You therefore don’t need to deal with selecting a special protocol for each brand or model device. (You do need to select a USB keyboard’s country codes, though.) The USB mouse protocol is modeled after that for PS/2 mice, so you can configure XFree86 just as you would for a PS/2 mouse, except that you specify a different device file.

USB connectors come in two varieties, known as Series A and Series B, both of which are shown in Figure 15.4. Motherboard USB ports normally accept Series A connectors, so this is the type you’ll find on mice. Some external devices, such as scanners and printers, often use detachable USB cables, and these devices often have Series B connectors.

![](img/860d0c38bd76c9ded976e9d1e179ef25_432_0.png)

**Figure 15.4** *You’ll find a Series A USB connector (left) on the end of a USB mouse or keyboard’s cable. Series B connectors (right) are used on external devices that use detachable USB cables.*
