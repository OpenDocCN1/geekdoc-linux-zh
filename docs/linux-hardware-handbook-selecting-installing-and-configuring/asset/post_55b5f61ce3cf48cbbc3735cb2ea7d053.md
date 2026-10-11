
- **MouseSystems** MouseSystems serial mice, and compatibles.
- **PS/2** PS/2 or USB mice. This protocol works with wheel mice, but doesn’t enable wheel functions. To enable wheel functions, use the IMPS/2 protocol instead. (The wheel’s button functionality still works with the plain PS/2 protocol, however.)

X supports additional, more exotic mouse protocols. Check the XF86Config man page for a complete list.

**NOTE**

Don’t assume that a mouse uses a protocol named after its manufacturer. Some Logitech serial mice, for instance, use the Microsoft protocol. All PS/2 mice use the PS/2 or IMPS/2 protocols, regardless of manufacturer.

If you have a wheel mouse, you must create custom configurations for each application or application type to map the wheel’s movement onto useful actions. These configurations generally go in your `~/.Xdefaults` file or an application-specific configuration file. As an example, here’s what you add to `~/.Xdefaults` to get programs that use the Athena widget set to recognize the scroll wheel:

```
#H Athena text widgets
*Panel.Text.translations: #override\n\n
Shift<Btn4Down>:<Btn4Up>: scroll-one-line-down()\n\n
Shift<Btn5Down>:<Btn5Up>: scroll-one-line-up()\n\n
Ctrl<Btn4Down>:<Btn4Up>: previous-page()\n\n
Ctrl<Btn5Down>:<Btn5Up>: next-page()\n\n
None<Btn4Down>:<Btn4Up>:scroll-one-line-down()scroll-one-line-down()\n\n
scroll-one-line-down()scroll-one-line-down()scroll-one-line-down()\n\n
None<Btn5Down>:<Btn5Up>:scroll-one-line-up()scroll-one-line-up()\n\n
scroll-one-line-up()scroll-one-line-up()scroll-one-line-up()
```

The Web site `http://www.inria.fr/~koala/colias/mouse-wheel-scroll/` is dedicated to collecting useful configurations for Linux programs to enable them to use mouse wheel features. This Web page also includes discussions of the quirks of specific wheel mouse models, so if you want to buy a wheel mouse and wheel functionality is high on your agenda, be sure to check this page for compatibility information.

## Summary

There’s very little about keyboard and mouse hardware that’s likely to pose problems for Linux. The main caveat is that support for USB devices is still weak in stock Linux distributions for x86 computers. You might need to use a standard keyboard for installing Linux, or choose your distribution with an eye for USB support. Keyboards don't vary a lot in their features, although their underlying technologies do differ and impact the keyboard feel. Pointing devices, on the other hand, vary substantially in function, ranging from conventional mice to TrackPoints. Each technology has its advantages and disadvantages, as well as adherents and detractors. The key is to choose a pointer that's comfortable to you. Fortunately, pointers are inexpensive enough that you can probably afford to try several types—but be aware that the ergonomically superior models of any given type are usually the more expensive ones.

## CHAPTER 16
Parallel and Serial Ports

### IN THIS CHAPTER

- Port Hardware Requirements 436
- A History of Ports in Linux 441
- Adding a Port 443
- USB: The Future of External Ports? 449

Traditionally, most external devices have interfaced to x86 computers through one of two types of port: an *RS-232 serial port* or a *parallel port*. Both ports are designed for general-purpose data communications, rather than for specific devices. Parallel ports have traditionally been used by printers, although in recent years these ports have taken on additional duties as a means of interfacing with external removable disk *drives*, Web *cams*, and so on.

These ports receive their names from their means of transmitting data. Serial ports use two data transmission lines, one in each direction. (There are also a number of control lines that aren't involved in the data transmission *per se* but that help regulate its flow.) On each line, data can be transmitted one bit at a time, so to transmit one byte (eight bits) worth of data, it's necessary to transmit the bits one after another—that is, in a *serial* manner. Parallel ports, by contrast, use eight data transfer lines, so it's possible to transmit an entire byte at once. The eight bits traverse the cable in *parallel* with one another.

All other things being equal, parallel ports are faster than serial ports, but parallel cables have more stringent length limits than serial cables. As technologies improve, it becomes possible to overcome both speed and cable length limits of the past. The latest form of serial port in use on x86 computers is known as the *Universal Serial Bus* (USB). USB is substantially faster than the earlier RS-232 serial ports, and it's much more flexible. It's *still* very new, however, so Linux support for USB devices is still maturing. I use the term *serial port* to mean the earlier RS-232 serial port. USB's practical differences make it as different from RS-232 serial as is parallel port technology.

**NOTE**

Other types of ports, such as SCSI ports (see Chapter 9, "SCSI Host Adapters") and keyboard ports (see Chapter 15, "Keyboards and Mice"), can be classified as being parallel or serial in nature. In this chapter, I am concerned only with the parallel printer port, RS-232 serial, and USB.

## Port Hardware Requirements

Parallel and serial ports both consume limited system resources—notably, interrupts and I/O ports. The specific interrupts and I/O ports used by specific serial and parallel ports is fairly well standardized, and is summarized in Table 16.1. I describe these requirements in greater detail shortly.

### **TABLE 16.1** Resources Used by Common Ports

| Port | Device File | Device Major | Device Minor | Interrupt | I/O Port |
|---|---|---|---|---|---|
| First Serial | `/dev/ttyS0` | 4 | 64 | 4 | 0x3f8–0x3ff |
| Second Serial | `/dev/ttyS1` | 4 | 65 | 3 | 0x2f8–0x2ff |
| Third Serial | `/dev/ttyS2` | 4 | 66 | 4$^1$ | 0x3f8–0x3ff$^1$ |
| Fourth Serial | `/dev/ttyS3` | 4 | 67 | 3$^1$ | 0x2f8–0x2ff$^1$ |
| First Parallel | `/dev/lp0^3` | 6 | 0 | 7$^2$ | 0x3bc–0x3bf |
| Second Parallel | `/dev/lp1^3` | 6 | 1 | 5$^2$ | 0x378–0x37a |
| Third Parallel | `/dev/lp2^3` | 6 | 2 | 5$^{1,2}$ | 0x278–0x27a |
| USB | Variable | Variable | Variable | Variable | Variable |

$^1$*This standard assignment is shared, and might not work well under Linux. If possible, assign another resource to avoid problems.*

$^2$*Use of an interrupt for parallel ports under Linux is optional.*

$^3$*This is the device filename used to access a printer via a parallel port. Access to other parallel devices can be done through other device files.*

## Interrupts

Interrupts (sometimes abbreviated *IRQs*, for *interrupt requests*) are used by devices to signal the computer that an important event has occurred, such as the receipt of data for processing. The x86 architecture allows for only 16 interrupts, numbered 0–15. One of these interrupts (number 2) is effectively unusable, because the x86 interrupt architecture uses two interrupt controllers, each of which can handle 8 interrupts. The second controller, which handles interrupts 8–15, requires an interrupt on the first controller to function, and the second controller uses IRQ 2 on the first controller for this purpose.

Each RS-232 serial port is assigned a standard interrupt number. Unfortunately, the standard assignment for ports beyond the second *shares* the interrupts between serial ports, as shown in Table 16.1. Sharing interrupts in this way works acceptably in DOS, but requires special configuration in Linux. Therefore, if you purchase an internal modem or secondary serial port card, you should do one of three things:

- Disable an unused serial port on the motherboard and configure the internal modem to use its port number. For instance, you could disable `/dev/ttyS0` (identified as **COM1**: in the BIOS) using your BIOS’s setup routines, and configure the modem to take on this identity.
- Enable the Support for sharing serial interrupts option under Character devices in the Linux kernel configuration. Doing so enables you to use a shared interrupt for serial ports.
- Assign the new port an interrupt other than the standard one. For instance, you might give it IRQ 9. The add-on device will then become `/dev/ttyS2` (and `/dev/ttyS3`, if it’s a two-port serial card and you give the second card its own interrupt, as well).

If you need more than two or three serial ports, I recommend you use a multiport serial board. These products support running several serial ports on just one interrupt, but they require special drivers in Linux. Fortunately, the Linux kernel includes the necessary drivers to support several multiport serial boards, so you should check the kernel configuration options to find which boards are supported.

By default, most Linux distributions are configured to not use interrupts for printing on the parallel ports. Instead, the hardware is operated in *polling mode*, which consumes more CPU time but leaves the parallel port’s interrupt available for use by other devices. If you want to switch to using an interrupt for a printer port, you can do so by copying the interrupt number to the `/proc/parport/n/irq` file, where *n* is the parallel port number. For instance, to change `/dev/lp0` to use interrupt 7, issue the following command:

```
echo 7 > /proc/parport/0/irq
```

You can confirm that this action has had the desired effect by typing `cat /proc/interrupts` and checking that interrupt 7 is used by the parallel port driver. You should then check to be sure you can print. If this change causes problems, you can reverse it by echoing the value 0 to the `/proc/parport/n/irq` file.

**Note**

Linux kernels prior to 2.1.131 used a different method of configuring interrupt-driven printing. These kernels used a program called *tunelp* to do the job. I describe this program later in this chapter.
